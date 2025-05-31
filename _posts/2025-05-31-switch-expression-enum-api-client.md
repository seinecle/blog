---
layout: post
title: Achieving free query params completeness check with native Java switch patter expressions on enums
permalink: /enum-completess-check-api-client/
published: false
date_readable:               May 31, 2025
last_modified_at_readable:   May 31, 2025
categories: [enum, pattern switch, web API, Java]
---


In a micro-service architecture where multiple API endpoints coordinate through requests sent and received: how to make sure to keep track and maintain the clients sending the requests, and the endpoints receiving these requests?

A large number of solutions exist to document and maintain these APIs, based on the [OpenAPI specification](https://spec.openapis.org/oas/v3.1.0).

Another road, supposedly lighter because it doesn't rely on OpenAPI, consists in creating an interface that will be shared across server and clients.

New Java language features offer a lightweight support on this issue.

# JDK 21+ completeness check on enums in switch expressions

In JDK 21+, the Java compiler now raises a warning if the values of an enum are not exhaustively listed in a switch expression.

So if you changed your list of query parameters server side but forgot to reflect this change on client' side, this will show and the client will stop compiling. Nice reminder!

Here is a hello world:

## create an enum for your query parameters
This enum should be in a module shared by your server and client.

``` java
public enum QueryParams {
        LANG, REPLACE_STOPWORDS, IS_SCIENTIFIC_CORPUS, LEMMATIZE, REMOVE_ACCENTS, PRECISION, MIN_CHAR_NUMBER, MIN_TERM_FREQ
    }
```

## client side
Add the params to your request by looping on the enum values.

``` java
for (QueryParams param : QueryParams.values()) {
            String paramValue = switch (param) {
                case LANG ->
                    selectedLanguage;
                case REPLACE_STOPWORDS ->
                    String.valueOf(replaceStopwords);
                case IS_SCIENTIFIC_CORPUS ->
                    String.valueOf(scientificCorpus);
                case LEMMATIZE ->
                    String.valueOf(lemmatize);
                case REMOVE_ACCENTS ->
                    String.valueOf(removeNonAsciiCharacters);
                case PRECISION ->
                    String.valueOf(precision);
                case MIN_CHAR_NUMBER ->
                    String.valueOf(minCharNumber);
                case MIN_TERM_FREQ ->
                    String.valueOf(minTermFreq);
            };
            requestBuilder.addQueryParameter(param.name(), paramValue);
        }
```

## server side
Things are not that simple there: The exhaustiveness check on enums happens only when a switch expression is used, not a switch statement.

Just to remind between the two:

**switch statement** -> when each case executes a block of code, without assigning a value

``` java
int dayOfWeek = 3;
String dayName;

switch (dayOfWeek) {
    case 1:
        dayName = "Monday";
        { // any code you want }
        break;
```

**switch statement** -> when each case assigns a value to the variable in the switch

``` java
int dayOfWeek = 3;
String dayName = switch (dayOfWeek) {
    case 1 -> "Monday";
```



``` java

        for (var entry : ctx.queryParamMap().entrySet()) {
            String key = entry.getKey();
            String decodedParamValue = URLDecoder.decode(entry.getValue().getFirst(), StandardCharsets.UTF_8);

            Consumer<String> qpHandler = switch (QueryParams.valueOf(key.toUpperCase())) {
                case LANG ->
                    workflow::setLang;
                case PRECISION ->
                    s -> workflow.setPrecision(Integer.parseInt(s));
                case MIN_TERM_FREQ ->
                    s -> workflow.setMinTermFreq(Integer.parseInt(s));
                case MIN_CHAR_NUMBER ->
                    s -> workflow.setMinCharNumber(Integer.parseInt(s));
                case REPLACE_STOPWORDS ->
                    s -> workflow.setReplaceStopwords(Boolean.parseBoolean(s));
                case REMOVE_ACCENTS ->
                    s -> workflow.setRemoveAccents(Boolean.parseBoolean(s));
                case LEMMATIZE ->
                    s -> workflow.setLemmatize(Boolean.parseBoolean(s));
                case IS_SCIENTIFIC_CORPUS ->
                    s -> workflow.setIsScientificCorpus(Boolean.parseBoolean(s));
            };
            qpHandler.accept(decodedParamValue);
```

# About
I’m an academic and independent web app developer. I created [nocode functions](https://nocodefunctions.com) 🔎, a free, point-and-click tool for exploring texts and networks. It’s [fully open source](https://github.com/seinecle/nocodefunctions). Try it out and let me know what you think. I’d love your feedback!

- **Email:** [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com) 📧  
- **Bluesky:** [@seinecle](https://bsky.app/profile/seinecle.bsky.social) 📱  
- **Blog:** [Read more articles](https://nocodefunctions.com/blog) 👓 on app development and data exploration.
