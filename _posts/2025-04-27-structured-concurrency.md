---
layout: post
title: La structured concurrency en Java
permalink: /java-structured-concurrency/
published: true
date_readable:               April 27, 2025
last_modified_at_readable:   April 27, 2025
categories: [asynch, virtual threads, blocking, concurrency, reactive programming]
---

Quand j’ai vu apparaître la *structured concurrency* en Java, j’ai failli passer à côté.  

Une nouvelle API pour lancer des threads, bon. Après tout, Java avait déjà ses *ExecutorService*, *Future*, *CompletableFuture*...

Au début, j'ai cru que la structured concurrency n'apportait que des raffinements : une manière plus propre d'orchestrer les flux synchrones et asynchrones dans l'API de concurrence existante.
Mais en creusant, je me suis rendu compte que c'était beaucoup plus radical : ce n'est pas une nouvelle manière de faire du synchrone ou de l'asynchrone. C'est la fin du besoin de l'asynchrone en Java 😮.

## Exemple : un même besoin traité de trois manières

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

La logique est éclatée entre les callbacks, et la gestion des erreurs est dispersée. Et si code est d'une grande beauté formelle avec sa logique non bloquante, en pratique je trouve ca impossible à debugger:
* les breakpoints de mon IDE favori ne se déclenchent pas comme il faut,
* pour une "région" de mon cod que je veux mettre en asynch, je me retrouve toujours à devoir transformer toutes mes méthodes en aval dans cette logique, et ca devient une charge cognitive très lourde, que je n'avais pas demandée !

### 2. Avec un traditionnel ExecutorService, pas asynch

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

* il faut penser à shutdown,
* l’exception est cachée dans ExecutionException,
*et si un service échoue, il faut faire le ménage soi-même.

Même en utilisant des virtual threads (Executors.newVirtualThreadPerTaskExecutor()), on reste avec un code sans vraie structure : pas de supervision automatique, pas d'annulation en cas d'erreur.


### 3. Avec Structured Concurrency

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

Avec cette nouvelle approche, on peut utiliser la concurrence sans devoir faire des numéros d’équilibriste :

* Est-ce que la tâche va créer des milliers de sous-tâches ?
* Faut-il choisir un Executor spécial ?
* Combien de threads faut-il prévoir ?

On n’a plus à se poser autant de questions.

On peut y aller beaucoup plus en confiance : démarrer des tâches, les superviser, attendre leur résultat, sans que le coût caché explose derrière.

# Où en est la Structured Concurrency aujourd'hui ?

La Structured Concurrency est arrivée en preview avec Java 21.

À fin avril 2025, elle est toujours en preview (avec quelques ajustements mineurs) dans Java 24.

Elle devrait être stabilisée et devenir officielle prochainement — mais elle est déjà totalement utilisable pour les projets qui ciblent un JDK récent.
