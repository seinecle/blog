---
layout: post
permalink: /java-structured-concurrency/
title: "Structured Concurrency en Java : Une Révolution Silencieuse"
date_readable:                 April 27, 2025
last_modified_at_readable:     April 27, 2025
published: true
categories: [java, concurrency, structured-concurrency, virtual-threads]
---

Quand j’ai vu apparaître la *structured concurrency* en Java, j’ai failli passer à côté.
Une nouvelle API pour lancer des threads, bon. Après tout, Java avait déjà ses *ExecutorService*, *Future*, *CompletableFuture*...

Mais en creusant, je me suis rendu compte que c’était beaucoup plus que ça. Ce n’est pas une nouvelle manière de faire de l’asynchrone. C’est la fin du besoin de l’asynchrone en Java.

## Un Même Besoin Traité de Trois Manières

Je veux appeler deux services en parallèle, récupérer leurs résultats, et propager les erreurs proprement. Trois approches possibles.

### 1. Approche avec `CompletableFuture`

```java
CompletableFuture<String> future1 = CompletableFuture.supplyAsync(() -> appelService1());
CompletableFuture<String> future2 = CompletableFuture.supplyAsync(() -> appelService2());

CompletableFuture<String> combined = future1.thenCombine(future2, (res1, res2) -> res1 + " " + res2);

combined
    .thenAccept(System.out::println)
    .exceptionally(ex -> {
        System.err.println("Erreur: " + ex.getMessage());
        return null;
    });

// Nécessite un sleep artificiel pour éviter la terminaison prématurée du programme
Thread.sleep(2000);
```

Cette approche fonctionne, mais elle requiert un sleep peu élégant pour empêcher la fin du programme avant l'exécution des tâches.
De plus, la logique est fragmentée dans les callbacks, et la gestion des erreurs est dispersée.

### 2. Approche avec ExecutorService
```java
ExecutorService executor = Executors.newFixedThreadPool(2);

Future<String> future1 = executor.submit(() -> appelService1());
Future<String> future2 = executor.submit(() -> appelService2());

String result1 = future1.get();
String result2 = future2.get();

System.out.println(result1 + " " + result2);

executor.shutdown();
```
Advanced

2.0 Flash


Conversation with Gemini
Garde ce blog post dans tout son format markdown. Corrige les titres et les commentaires qui sont assez "sloppy" pour décrire les 3 modes de code concurrent:

---

layout: post

permalink: /java-structured-concurrency/

title: "Structured concurrency en Java : une révolution silencieuse"

date_readable:               April 27, 2025

last_modified_at_readable:   April 27, 2025

published: true

categories: [java, concurrency, structured-concurrency, virtual-threads]

---



Quand j’ai vu apparaître la *structured concurrency* en Java, j’ai failli passer à côté.  

Une nouvelle API pour lancer des threads, bon. Après tout, Java avait déjà ses *ExecutorService*, *Future*, *CompletableFuture*...



Mais en creusant, je me suis rendu compte que c’était beaucoup plus que ça. Ce n’est pas une nouvelle manière de faire de l’asynchrone. C’est la fin du besoin de l’asynchrone en Java.



## Un même besoin traité de trois manières



Je veux appeler deux services en parallèle, récupérer leurs résultats, et propager les erreurs proprement. Trois approches possibles.



### 1. Avec `CompletableFuture`



```java

CompletableFuture<String> future1 = CompletableFuture.supplyAsync(() -> appelService1());

CompletableFuture<String> future2 = CompletableFuture.supplyAsync(() -> appelService2());



CompletableFuture<String> combined = future1.thenCombine(future2, (res1, res2) -> res1 + " " + res2);



combined

    .thenAccept(System.out::println)

    .exceptionally(ex -> {

        System.err.println("Erreur: " + ex.getMessage());

        return null;

    });



// Sleep pour éviter que le programme se termine trop vite

Thread.sleep(2000);

```



Ça marche, mais il faut du sleep bricolé pour éviter que tout se termine avant.

La logique est éclatée entre les callbacks, et la gestion des erreurs est dispersée.



2. Avec ExecutorService



```java

ExecutorService executor = Executors.newFixedThreadPool(2);



Future<String> future1 = executor.submit(() -> appelService1());

Future<String> future2 = executor.submit(() -> appelService2());



String result1 = future1.get();

String result2 = future2.get();



System.out.println(result1 + " " + result2);



executor.shutdown();

```



C’est plus propre que l’asynchrone pur. Mais :



il faut penser à shutdown,



l’exception est planquée dans ExecutionException,



et si un service échoue, il faut faire le ménage soi-même.





Même en utilisant des virtual threads (Executors.newVirtualThreadPerTaskExecutor()), on reste avec un code sans vraie structure : pas de supervision automatique, pas d'annulation en cas d'erreur.



3. Avec Structured Concurrency



```java

try (var scope = new StructuredTaskScope.ShutdownOnFailure()) {

    var task1 = scope.fork(() -> appelService1());

    var task2 = scope.fork(() -> appelService2());



    scope.join();

    scope.throwIfFailed();



    String result1 = task1.get();

    String result2 = task2.get();

  

  System.out.println(result1 + " " + result2);

}

```



Le code redevient séquentiel.

Pas de shutdown à penser.

Si une tâche échoue, tout est annulé proprement.



Et sous le capot : des virtual threads, donc aussi rapide qu’un code non bloquant, mais beaucoup plus lisible.



---



Avec cette nouvelle approche, on peut utiliser la concurrence sans devoir faire des numéros d’équilibriste :



Est-ce que la tâche va créer des milliers de sous-tâches ?



Faut-il choisir un Executor spécial ?



Combien de threads faut-il prévoir ?





On n’a plus à se poser autant de questions.

On peut y aller beaucoup plus en confiance : démarrer des tâches, les superviser, attendre leur résultat, sans que le coût caché explose derrière.





---



# Où en est la Structured Concurrency aujourd'hui ?



La Structured Concurrency est arrivée en preview avec Java 21.

À fin avril 2025, elle est toujours en preview (avec quelques ajustements mineurs) dans Java 22.

Elle devrait être stabilisée et devenir officielle prochainement — mais elle est déjà totalement utilisable pour les projets qui ciblent un JDK récent.




Markdown

---
layout: post
permalink: /java-structured-concurrency/
title: "Structured Concurrency en Java : Une Révolution Silencieuse"
date_readable:                 April 27, 2025
last_modified_at_readable:     April 27, 2025
published: true
categories: [java, concurrency, structured-concurrency, virtual-threads]
---

Quand j’ai vu apparaître la *structured concurrency* en Java, j’ai failli passer à côté.
Une nouvelle API pour lancer des threads, bon. Après tout, Java avait déjà ses *ExecutorService*, *Future*, *CompletableFuture*...

Mais en creusant, je me suis rendu compte que c’était beaucoup plus que ça. Ce n’est pas une nouvelle manière de faire de l’asynchrone. C’est la fin du besoin de l’asynchrone en Java.

## Un Même Besoin Traité de Trois Manières

Je veux appeler deux services en parallèle, récupérer leurs résultats, et propager les erreurs proprement. Trois approches possibles.

### 1. Approche avec `CompletableFuture`

```java
CompletableFuture<String> future1 = CompletableFuture.supplyAsync(() -> appelService1());
CompletableFuture<String> future2 = CompletableFuture.supplyAsync(() -> appelService2());

CompletableFuture<String> combined = future1.thenCombine(future2, (res1, res2) -> res1 + " " + res2);

combined
    .thenAccept(System.out::println)
    .exceptionally(ex -> {
        System.err.println("Erreur: " + ex.getMessage());
        return null;
    });

// Nécessite un sleep artificiel pour éviter la terminaison prématurée du programme
Thread.sleep(2000);
Cette approche fonctionne, mais elle requiert un sleep peu élégant pour empêcher la fin du programme avant l'exécution des tâches.
De plus, la logique est fragmentée dans les callbacks, et la gestion des erreurs est dispersée.

2. Approche avec ExecutorService
Java

ExecutorService executor = Executors.newFixedThreadPool(2);

Future<String> future1 = executor.submit(() -> appelService1());
Future<String> future2 = executor.submit(() -> appelService2());

String result1 = future1.get();
String result2 = future2.get();

System.out.println(result1 + " " + result2);

executor.shutdown();
Cette méthode est plus structurée que l'approche asynchrone pure. Cependant :

Il est impératif de penser à arrêter l'ExecutorService (shutdown).
Les exceptions sont enveloppées dans une ExecutionException, ce qui complexifie leur traitement.
En cas d'échec d'un service, une gestion manuelle est nécessaire pour nettoyer les ressources.
Même en utilisant des virtual threads avec Executors.newVirtualThreadPerTaskExecutor(), le code manque de structure intrinsèque : absence de supervision automatique et d'annulation coordonnée en cas d'erreur.

3. Approche avec Structured Concurrency
Java

try (var scope = new StructuredTaskScope.ShutdownOnFailure()) {
    var task1 = scope.fork(() -> appelService1());
    var task2 = scope.fork(() -> appelService2());

    scope.join();
    scope.throwIfFailed();

    String result1 = task1.get();
    String result2 = task2.get();

    System.out.println(result1 + " " + result2);
}
Le code retrouve une structure séquentielle claire.
La gestion de l'arrêt (shutdown) devient automatique grâce au try-with-resources.
En cas d'échec d'une tâche, toutes les autres sont annulées proprement.

De plus, sous le capot, l'utilisation de virtual threads garantit des performances comparables à du code non bloquant, tout en offrant une lisibilité accrue.

Avec cette nouvelle approche, il devient possible d'exploiter la concurrence sans les complexités habituelles :

Faut-il anticiper la création de milliers de sous-tâches ?
Est-il nécessaire de choisir un Executor spécifique ?
Combien de threads faut-il provisionner ?
Ces questions deviennent moins prégnantes.
L'on peut aborder la concurrence avec une confiance accrue : démarrer des tâches, les superviser, attendre leurs résultats, sans craindre une explosion des coûts cachés.

État Actuel de la Structured Concurrency
La Structured Concurrency a été introduite en preview avec Java 21.
Fin avril 2025, elle demeure en preview (avec quelques ajustements mineurs) dans Java 22.
Sa stabilisation et son adoption officielle devraient être imminentes — elle est cependant déjà pleinement utilisable pour les projets ciblant un JDK récent.


Reformate ta réponse pour que je puisse la copier coller en markdown en entier



Markdown

---
layout: post
permalink: /java-structured-concurrency/
title: "Structured Concurrency en Java : Une Révolution Silencieuse"
date_readable:                 April 27, 2025
last_modified_at_readable:     April 27, 2025
published: true
categories: [java, concurrency, structured-concurrency, virtual-threads]
---

Quand j’ai vu apparaître la *structured concurrency* en Java, j’ai failli passer à côté.
Une nouvelle API pour lancer des threads, bon. Après tout, Java avait déjà ses *ExecutorService*, *Future*, *CompletableFuture*...

Mais en creusant, je me suis rendu compte que c’était beaucoup plus que ça. Ce n’est pas une nouvelle manière de faire de l’asynchrone. C’est la fin du besoin de l’asynchrone en Java.

## Un Même Besoin Traité de Trois Manières

Je veux appeler deux services en parallèle, récupérer leurs résultats, et propager les erreurs proprement. Trois approches possibles.

### 1. Approche avec `CompletableFuture`

```java
CompletableFuture<String> future1 = CompletableFuture.supplyAsync(() -> appelService1());
CompletableFuture<String> future2 = CompletableFuture.supplyAsync(() -> appelService2());

CompletableFuture<String> combined = future1.thenCombine(future2, (res1, res2) -> res1 + " " + res2);

combined
    .thenAccept(System.out::println)
    .exceptionally(ex -> {
        System.err.println("Erreur: " + ex.getMessage());
        return null;
    });

// Nécessite un sleep artificiel pour éviter la terminaison prématurée du programme
Thread.sleep(2000);
```

Cette approche fonctionne, mais elle requiert un sleep peu élégant pour empêcher la fin du programme avant l'exécution des tâches.
De plus, la logique est fragmentée dans les callbacks, et la gestion des erreurs est dispersée.

### 2. Approche avec ExecutorService

``` Java
ExecutorService executor = Executors.newFixedThreadPool(2);

Future<String> future1 = executor.submit(() -> appelService1());
Future<String> future2 = executor.submit(() -> appelService2());

String result1 = future1.get();
String result2 = future2.get();

System.out.println(result1 + " " + result2);

executor.shutdown();
```
Cette méthode est plus structurée que l'approche asynchrone pure. Cependant :

Il est impératif de penser à arrêter l'ExecutorService (shutdown).
Les exceptions sont enveloppées dans une ExecutionException, ce qui complexifie leur traitement.
En cas d'échec d'un service, une gestion manuelle est nécessaire pour nettoyer les ressources.
Même en utilisant des virtual threads avec Executors.newVirtualThreadPerTaskExecutor(), le code manque de structure intrinsèque : absence de supervision automatique et d'annulation coordonnée en cas d'erreur.

### 3. Approche avec Structured Concurrency
``` java
try (var scope = new StructuredTaskScope.ShutdownOnFailure()) {
    var task1 = scope.fork(() -> appelService1());
    var task2 = scope.fork(() -> appelService2());

    scope.join();
    scope.throwIfFailed();

    String result1 = task1.get();
    String result2 = task2.get();

    System.out.println(result1 + " " + result2);
}
```
