---
layout: post
title: Concurrency and decoupling for cheap with Java 11 HttpClient asynch requests
permalink: /java-concurrency-with-http-client-asynch/
published: true
date_readable:               Feb 19, 2022
last_modified_at_readable:   Feb 19, 2022
---

_After years of dabbling with `threads`, `Callables` and `Executor Pools`, finally an easy way to setup concurrent tasks_

# The problem: having a task to execute concurrently, but keeping the code free from Callables and other thread logic

For many years, I have worked at making some parts of my code execute in a concurrent way. Pair-wise computations on vectors, text mining ops on thousands on tweets, simple checks and operations on nodes and edges in a network, etc.

The approach I took is pretty textbook, I suppose:

* isolate in a separate class the part of the code that can be executed concurrently: that will be the task.
* make this class implement the `Runnable` interface, or more probably the `Callable` interface as it allows to return an object.
* in the main part of the code, setup an `Executor` service. Instantiate all the tasks and submit these to the executor.
* collect the `Future` objects and aggregate their results.

I suppose there is nothing wrong with this. In practice, it didn't work for me. The reason is fundamentally that:

* setting the task as a `Runnable` or `Callable`, even if that is pretty easy and lightweight, specializes the code for this use case. If I want to re-use the code in another context that requires the logic to run with different interfaces, or refactor the task because the code logic has grown in complexity, these interfaces I had added for concurrency become boilerplate. I'm like "oh, I had added that `Callable` way of running the code for this particular project, but in this other project that's just a thing in my way. I'll have to remove it." So in practice, when I developped some concurrent code, I ended up giving up on it soon to work unencumbered.

* Setting up the `Executor` / `Future` logic on the main side of the code base is harder than it seems. There are so many variations on these APIs that it is a big effort each time to remember and identify how the thing should be set up. That is because multithreading and concurrency is low level, and one could be tempted to says that "there is a library that wraps this up for you". But I would really avoid relying on libraries for concurrency, they are probably super big and too wide in scope for what I want to do.

__Anyway, all this introduction to say that I've found a better way.__

It doesn't involve clever nor sophisticated tricks, so don't expect a big "wow". It is all in simplicity and robustness, and made very easy since Java 11's HttpClient.

# The solution: putting the task behind a REST API and calling it with Java 11's HttpClient asynch requests

The solution consists in:

* isolating the task in a separate module
* having this task called with a REST API, returning an Object
* in the main code base, calling each task with Java 11's HttpClient, using the asynch feature. __That's where concurrency kicks in!!__
* collecting the results

# Showing the code: the main code base

The use case consists in performing sentiment analysis on thousands of tweets. Instead of doing it sequentially, this can be done in a concurrent way.

* __Input__: each line of text (each tweet) is stored as a `String` with an `Integer` which is a unique identifier, in the form of an object `Map<Integer, String> mapOfLines`.
* __Output__: each line of text, its unique identifier, and the sentiment that was found, is stored in a `Document` object, itself stored in a object `ConcurrentHashMap<Integer, Document> tempResults`. The Map has to be a ConcurrentHashMap as it will be written to by many threads.

This is how the code looks like:

```java
String selectedLanguage = "en";

Map<Integer, String> mapOfLines = new HashMap();

mapOfLines.put(0, "This is a test. Concurrency is amazing!");
mapOfLines.put(1, "This is a test. Concurrency is hard!");

ConcurrentHashMap<Integer, Document> tempResults = new ConcurrentHashMap();

HttpRequest request;
HttpClient client = HttpClient.newHttpClient();

Set<CompletableFuture> futures = new HashSet();
			
// this is a convenient class I designed to clock time, available here https://github.com/seinecle/Utils			
Clock clock = new Clock("clocking the concurrent task");

try {
	for (Map.Entry<Integer, String> entry : mapOfLines.entrySet()) {
	
		Document doc = new Document();
		doc.setText(entry.getValue());
		doc.setId(entry.getKey());
		doc.setSentiment(Category._10);

		URI uri = new URI("http://localhost:45/api/sentimentForAText/" 
		+ selectedLanguage
		+ "?id="
		+ doc.getId() 
		+ "&text=" 
		+ URLEncoder.encode(entry.getValue(), StandardCharsets.UTF_8.toString()));

		request = HttpRequest.newBuilder()
				.uri(uri)
				.build();

		CompletableFuture<Void> future = client.sendAsync(request, HttpResponse.BodyHandlers.ofString())
		.thenAccept(resp -> {
			String body = resp.body();

			// the task returns a JSON Object, for convenience of handling
			
			// as you see below, it is very easy and convenient to define operations
			// on the body (here, a String) returned by each concurrent task 
			
			JsonReader jsonReader = Json.createReader(new StringReader(body));
			JsonObject jsonObject = jsonReader.readObject();
			Document docReturn = new Document();
			if (jsonObject != null && !jsonObject.isEmpty()) {

				String key = jsonObject.keySet().iterator().next();
				docReturn.setId(Integer.valueOf(key));
				docReturn.setText(mapOfLines.get(Integer.valueOf(key)));

				// Category._11 is the label for "positive sentiment" 
				if (jsonObject.getString(key).equals(Category._11.toString())) {
					docReturn.setSentiment(Categories.Category._11);
				}

				// Category._12 is the label for "negative sentiment" 
				if (jsonObject.getString(key).equals(Category._12.toString())) {
					docReturn.setSentiment(Categories.Category._12);
				}
				
				tempResults.put(Integer.valueOf(key), docReturn);
			}
		}
		);
		futures.add(future);

	}
	CompletableFuture<Void> combinedFuture = CompletableFuture.allOf(futures.toArray((new CompletableFuture[0])));
	combinedFuture.join();
	
	// tempResults ready to be use further in the code!

} catch (URISyntaxException exception) {
	System.out.println("URI syntax exception"+ exception);
} catch (UnsupportedEncodingException ex) {
	System.out.println("Encoding exception: "+ ex);
}

clock.closeAndPrintClock();
```

# Showing the code: the task

The task is behind a simple REST API, using the super lightweight Javalin framework (but any other REST framework would work). This code resides in a separate Java SE project, which compiles in a jar that I can deploy anywhere and separately from the main code base:

```java
public class APIController {

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {
    
        Javalin app = Javalin.create().start(45);
        System.out.println("running the api");
	
	// initialization of objects for sentiment analysis, just once when deploying the jar.
	// each call to the API will find these objects ready to use, that speeds things up.
	// this sentiment analyis tool is free and open source at: https://github.com/seinecle/umigon-core

	UmigonController umigonController = new UmigonController();
        ClassifierMachineOneDocument classifierOneDocEN = new ClassifierMachineOneDocument(umigonController.getSemanticsEN());
        ClassifierMachineOneDocument classifierOneDocFR = new ClassifierMachineOneDocument(umigonController.getSemanticsFR());

        app.get("/api/sentimentForAText/{lang}", ctx -> {
            JsonObjectBuilder objectBuilder = Json.createObjectBuilder();

	    String text = ctx.queryParam("text");
            String id = ctx.queryParam("id");
            if (id == null){
                id = UUID.randomUUID().toString().substring(0, 10);
            }
            if (text == null) {
                objectBuilder.add(id, "text parameter was absent");
                JsonObject jsonObject = objectBuilder.build();
                ctx.result(jsonObject.toString()).status(HttpCode.BAD_REQUEST);
            } else {
                String lang = ctx.pathParam("lang");
                Document doc = new Document();
                doc.setText(text);
                switch (lang) {
                    case "en":
                        doc = classifierOneDocEN.call(doc);
                        break;

                    case "fr":
                        doc = classifierOneDocFR.call(doc);
                        break;

                    default:
                        objectBuilder.add("-99", "wrong param for lang - lang not supported");
                        JsonObject jsonObject = objectBuilder.build();
                        ctx.result(jsonObject.toString()).status(HttpCode.BAD_REQUEST);
                }
                objectBuilder.add(id, doc.getSentiment().toString());
                JsonObject jsonObject = objectBuilder.build();

                ctx.result(jsonObject.toString()).status(HttpCode.OK);
            }
        }
        );
    }
```

# The argument for this design

Looking at the code above, I realize that the reaction might be whaaaat but this code is actually much more complex than using an `ExecutorService` etc! Well, let's examine the pros and cons:

## Pros

* the task is completely free from the concurrency logic. No `Callable` nor `Runnable`. That frees your mind!
* it follows that the task is completely reusable and can be refactored without a consequence on the logic of concurrency, from the perspective of the main code base. Huge bonus, as you don't want to be disturbed, when working on the logic of your code, by problems of making the code "concurrent compatible".
* the encapsulation behind a REST API is a bonus:
	1. you get an API!
	2. the codebase for the task is the same across interfaces. In practice, the sentiment analyis task is carried out by the same code on the web app interface and the API, visible here: https://nocodefunctions.com/umigon/sentiment_analysis_tool.html
	3. the task is offloaded from the main codebase, and that helps make things more organized
* calling the concurrent tasks from the main codebase is _relatively_ simple. Not need to instantiate or fiddle with an `Executor`, as it comes already bundled in the HttpClient. But it can be taylored if needed.

## Cons

* using json to carry the response of the task back to the main code base makes things brittle. I might need to change the Json format on the REST API side, and forget to update the way the `JSON Object` is read on the main code base.
* do you see any other disadvantage?

## Gains and possible limits

* __Speed__: on a multi-core machine, execution times are 4x to 6x faster than a sequential execution.
*  __Limits__:
	1. Local vs remote: the gains of concurrency as shown above are achieved when the REST API sits on the same machine as the main code base. When I tried the mix (main code base on local laptop x REST API on a distante server), the code was just suuuuper slow. I didn't investigate why.
	2. When the REST API is on a Windows Machine, there is a maximum limit of connections. Hitting this limit causes an exception. Weird! So make sure to host your REST API on linux.

### Conclusion and thanks
I will progressively refactor all the functions on [nocodefunctions.com](https://nocodefunctions.com) to adopt this design. At the moment (Feb 19, 2022), only [sentiment analysis](https://test.nocodefunctions.com/umigon/sentiment_analysis_tool.html) on the _test_ version of the site has been implemented. As a result, analyzing 6,000 tweets take just 10 seconds now (600 tweets per second!), versus ~ one minute before.

I arrived at this solution after reading many blog posts by professional Java developers and StackOverflow Q&As. I thank all these contributors, and I hope this new blog post will be of help to the next person researching these topics.
