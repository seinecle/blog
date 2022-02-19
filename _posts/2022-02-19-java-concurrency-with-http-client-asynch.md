---
layout: post
title: Concurrency and decoupling for cheap with Java 11 HttpClient asynch requests
permalink: /java-concurrency-with-http-client-asynch/
published: false
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

It doesn't involve clever nor sophisticated tricks, so don't expect a big "wow". It is all in simplicity and robustness. 

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
            Map<Integer, String> mapOfLines = new HashMap();
	
			mapOfLines.put(0, "This is a test. Concurrency is amazing!");
			mapOfLines.put(1, "This is a test. Concurrency is hard!");
			
			ConcurrentHashMap<Integer, Document> tempResults = new ConcurrentHashMap();

            HttpRequest request;
            HttpClient client = HttpClient.newHttpClient();
            Set<CompletableFuture> futures = new HashSet();
			
            Clock clock = new Clock("clocking the concurrent task");

            try {
                for (Map.Entry<Integer, String> entry : mapOfLines.entrySet()) {
                    Document doc = new Document();
                    doc.setText(entry.getValue());
                    doc.setId(entry.getKey());
                    doc.setSentiment(Category._10);

                    URI uri = new URI("http://localhost:7002/api/sentimentForAText/" + selectedLanguage + "?id=" + doc.getId() + "&text=" + URLEncoder.encode(entry.getValue(), StandardCharsets.UTF_8.toString()));

                    request = HttpRequest.newBuilder()
                            .uri(uri)
                            .build();

                    CompletableFuture<Void> future = client.sendAsync(request, HttpResponse.BodyHandlers.ofString()).thenAccept(resp -> {
                        String body = resp.body();

						// the task returns a JSON Object, for convenience of handling
						
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

* in supervised learning, labeled datasets provide a ground for the model to train on. Good annotations make good training sets, which impact greatly the quality of the model.
* in models that are "rule based", a dataset which is accurately labeled makes sure the rules and heuristics get triggered in the appropriate circumstances.

Annotating data consists for a person to point the absence or presence of a specific feature in a piece of text, an image, a video or audio content...
For instance, the open source solution Label Studio offers tools to annotate audio segments, by adding tags [in a very intuitive interface](https://labelstud.io/playground/){:target="_blank"}:

<div align="center">
   <img src="https://user-images.githubusercontent.com/1244100/151705003-f9c8212c-e76e-4550-8926-8605ca7c307f.png" width="400"/>
</div>

# How are annotations managed, in practice?

Until ~ 2015, Amazon Mechanical Turk ([MTurk](https://www.mturk.com/)) was the dominant solution to design tasks and crowd-source them to people recruited on the same platform.
It has profoundly changed practices in the industry, and in academia as well.
In 2016, 43% of behavioral studies featured in the academic _Journal of Consumer Behavior_ were conducted on MTurk! ([^1])

This position evolved:

- new actors emerged, integrating additional services
- some actors positioned themselves on a specific segment: crowd-sourcing __annotation__ tasks.

Today, querying "annotation platform" on your favorite search engine will return the names of [Toloka](https://toloka.ai), [SuperAnnotate](https://www.superannotate.com), [Basic.ai](https://www.basic.ai), and many more.

<div align="center">
   <img src="https://user-images.githubusercontent.com/1244100/151705453-f40cea8d-f5c9-4e86-8dcb-1ef3a2463718.png"/>
  <br/>
   <img src="https://user-images.githubusercontent.com/1244100/151705550-5533fd1e-5fcc-4b55-a52f-6a8784e03aec.png"/>
  <br/>
   <img src="https://user-images.githubusercontent.com/1244100/151705567-89e2e755-d1d2-48da-ac31-c2ce77e48207.png"/>
  <br/>
   <img src="https://user-images.githubusercontent.com/1244100/151705592-3f521256-8f98-4966-874d-5c40819b1ec8.png"/>
  <br/>
   <img src="https://user-images.githubusercontent.com/1244100/151705611-c21b9cde-bc08-4462-9f77-df1cd219b676.png"/>
  <br/>
   <img src="https://user-images.githubusercontent.com/1244100/151705768-4667a2fe-b5ea-4b8b-95f3-94af1854c3b7.png"/>
</div>  
<br/>

Together, these companies and products coalesce into a new, specific industy proposing part or all of:

- tools for annotating text, image, video, audio
- project management (curation, quality control, time management, data security, etc.)
- management of the workforce of annotators - including the setup of world-wide marketplaces
- integration with the rest of the flow of data analysis
- with industry-specific features ([DiscoverText](https://www.discovertext.com/), for example, is well suited for academic needs and Twitter data)

Amazon has followed up these developments by adding an "[Amazon SageMaker Data Labeling](https://aws.amazon.com/sagemaker/data-labeling/?nc=sn&loc=0)" (aka Amazon SageMaker Ground Truth Plus) to their MTurk offer.


# Considering all this, why did I add an annotation tool to [Nocode functions](https://nocodefunctions.com/)?

Isn't it very redundant, given the plethora of offer? These are the reasons:

1. To be effective, annotation tasks need to be precisely taylored to the case.
2. A third party solution can be hard to fit in an existing chain of data processing

These two points boil down to "customization". I need to run annotation tasks in ways that are not covered by the existing solutions. Specifically:

- I need to run a Best-Worst Scaling task. This is suuuuper powerful and yet not on offer anywhere AFAIK. So I added [BWS Tasks](https://nocodefunctions.com/blog/best-worst-scaling-bws-in-progress/) to Nocode functions, for my own use and for anyone else with the same need.
- I need to categorize words, which is a super classic kind of task. But these words need to be highlighted in a sentence, to provide context to the annotator. Otherwise, how can the annotator judge the meaning of a word in isolation? That would be much harder and imprecise. So I need a task that allows a notion like: "annotate an object, which has a value (the word) and a 'displayed' value for the annotator (a sentence where the term appears, with some css to highlight it)".  For instance, to categorize the term "Oklahoma" I would need it to be inserted in a sentence for context, with some color effect to signal it to the annotator:

"To the red country and part of the gray country of <span id="oklahoma">Oklahoma</span>, the last rains came gently, and they did not cut the scarred earth."

I developed a specific [function to do this highlighting](https://nocodefunctions.com/highlighter/highlight_word_in_context.html), so that  now [tasks on Nocode function have the notion of item value / item displayed value with css formatting for the annotation of an item](https://nocodefunctions.com/labelling/role.html).
- While the above seems trivial (adding some css...), it has cascading impacts on the UI. For instance, the solution now needs to allow for the import of two fields per item to annotate (the value of the item, and the displayed value with the css). This can be managed by defining a json schema for the data to be imported... but that would add another layer of complexity and pre-supposes the task designer is comfortable with a programmatic approach. I choose instead to have a click-and-point interface where two columns can be imported from a csv or Excel spreadsheet: one for the term, one for the sentence where the term is embedded. Very simple.

Yes, this is not industry-grade so I don't expect it to be widely adopted. I just hope that it will improve the quality of the annotations for my research and that it will prove useful to small teams that need these functions specifically, without lock-in nor the complexity of adopting large scale solutions.

As always, [your feedback is welcome](https://nocodefunctions.com/support.html)!

[^1]: [ Joseph K Goodman & Gabriele Paolacci (2017): Crowdsourcing Consumer Research](https://doi.org/10.1093/jcr/ucx047).
