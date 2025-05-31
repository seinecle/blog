---
layout: post
title: Free Completeness Checks for Query Params with Java Enum Switch Expressions
permalink: /enum-completeness-check-api-client/
published: true
date_readable: May 31, 2025
last_modified_at_readable: May 31, 2025
categories: [enum, pattern switch, web API, Java]
---

When maintaining APIs with multiple clients and endpoints, how can you ensure consistency between the query parameters defined on the server and those implemented by clients?

A common solution is to document and maintain APIs using the [OpenAPI specification](https://spec.openapis.org/oas/v3.1.0), implemented by many frameworks. However, if you're looking for a simpler, framework-free alternative, recent Java language features offer built-in support to ensure consistency through exhaustiveness checks on enums in switch expressions.

# Completeness checks on enums using JDK 21+ switch expressions

From JDK 21 onwards, the Java compiler enforces exhaustiveness checks in `switch` expressions involving enums. This means the compiler will raise an error if an enum value is omitted from a switch statement.

This feature ensures consistency: if you modify the query parameters on the server but forget to update the client, the client-side code will not compile, serving as an effective safeguard.

Here's a practical example:

## Defining an enum for your query parameters

Place this `enum` in a shared module accessible by both the server and client:

```java
public enum QueryParams {
    LANG, REPLACE_STOPWORDS, IS_SCIENTIFIC_CORPUS, LEMMATIZE, REMOVE_ACCENTS, PRECISION, MIN_CHAR_NUMBER, MIN_TERM_FREQ
}
```

## Client-side implementation

Loop over the enum values to add query parameters to your request:

```java
for (QueryParams param : QueryParams.values()) {
    String paramValue = switch (param) {
        case LANG -> selectedLanguage;
        case REPLACE_STOPWORDS -> String.valueOf(replaceStopwords);
        case IS_SCIENTIFIC_CORPUS -> String.valueOf(scientificCorpus);
        case LEMMATIZE -> String.valueOf(lemmatize);
        case REMOVE_ACCENTS -> String.valueOf(removeNonAsciiCharacters);
        case PRECISION -> String.valueOf(precision);
        case MIN_CHAR_NUMBER -> String.valueOf(minCharNumber);
        case MIN_TERM_FREQ -> String.valueOf(minTermFreq);
    };
    requestBuilder.addQueryParameter(param.name(), paramValue);
}
```

## What happens if a parameter is omitted?

If you forget to handle a parameter, such as "PRECISION," the compiler will issue an error:

![Compiler Error](https://github.com/user-attachments/assets/bf0e763b-ddbf-43e5-bf6e-d1143b18935a)

My IDE (NetBeans) provides a helpful warning explaining the issue:

![IDE Warning](https://github.com/user-attachments/assets/d423f17d-413b-4d53-aeb7-5aef533fadde)

## Server-side implementation

The server-side code follows the same principle. It will also generate compiler errors if any enum values are missing in your switch statements.

Here’s an interesting server-side twist: in my application, query parameters are parsed into values set within a workflow object. To maintain the exhaustiveness checks while parsing parameters, ChatGPT suggested the elegant solution of using a `Consumer`:

```java
private static RunnableTopicsWorkflow parseQueryParams(RunnableTopicsWorkflow workflow, Map<String, List<String>> queryParamMap) throws Exception {
    for (var entry : queryParamMap.entrySet()) {
        String key = entry.getKey();
        String decodedParamValue = URLDecoder.decode(entry.getValue().getFirst(), StandardCharsets.UTF_8);

        Consumer<String> qpHandler = switch (QueryParams.valueOf(key.toUpperCase())) {
            case LANG -> workflow::setLang;
            case PRECISION -> s -> workflow.setPrecision(Integer.parseInt(s));
            case MIN_TERM_FREQ -> s -> workflow.setMinTermFreq(Integer.parseInt(s));
            case MIN_CHAR_NUMBER -> s -> workflow.setMinCharNumber(Integer.parseInt(s));
            case REPLACE_STOPWORDS -> s -> workflow.setReplaceStopwords(Boolean.parseBoolean(s));
            case REMOVE_ACCENTS -> s -> workflow.setRemoveAccents(Boolean.parseBoolean(s));
            case LEMMATIZE -> s -> workflow.setLemmatize(Boolean.parseBoolean(s));
            case IS_SCIENTIFIC_CORPUS -> s -> workflow.setIsScientificCorpus(Boolean.parseBoolean(s));
        };
        qpHandler.accept(decodedParamValue);
    }
    return workflow;
}
```

# See this approach implemented in production
I am currently refactoring nocodefunctions.com to implement this approach. Check:

- the [repo for the frontend of the app](https://github.com/seinecle/nocodefunctions-web-app), which builds requests sent to the microservices
- the [portal for microservices](https://github.com/seinecle/nocodefunctions-as-api), receiving these requests
- the [module](https://github.com/seinecle/function-model) shared between the frontend and the portal


# About
I’m an academic and independent web app developer. I created [nocode functions](https://nocodefunctions.com) 🔎, a free, point-and-click tool for exploring texts and networks. It’s [fully open source](https://github.com/seinecle/nocodefunctions). Try it out and let me know what you think—I’d love your feedback!

* **Email:** [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com) 📧
* **Bluesky:** [@seinecle](https://bsky.app/profile/seinecle.bsky.social) 📱
* **Blog:** [Read more articles](https://nocodefunctions.com/blog) 👓 on app development and data exploration.
