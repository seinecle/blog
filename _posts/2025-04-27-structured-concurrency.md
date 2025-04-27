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

Si code est d'une grande beauté formelle avec sa logique chaînée réactive / non bloquante.

Mais en pratique je trouve ca impossible à debugger:

* les breakpoints de mon IDE favori ne se déclenchent pas comme il faut,
* pour une "région" de mon code que je veux mettre en async, je me retrouve toujours à devoir transformer toutes mes méthodes en aval dans cette logique, et ca devient une charge cognitive très lourde, que je n'avais pas demandée !

Et puis, le chaînage des méthodes (then... combine... exceptionnally...) qui est encore une fois une promesse d'élégance et de structuration, finit par faire du code très indenté et complexe. Les statements séquentiels ont du bon, en vrai !

### 2. Avec un traditionnel ExecutorService, pas async

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
* l’exception est cachée dans ExecutionException
*et si un service échoue, il faut faire le ménage soi-même.

Même en utilisant des virtual threads ('Executors.newVirtualThreadPerTaskExecutor()'), on reste avec un code sans vraie structure : pas de supervision automatique, pas d'annulation en cas d'erreur.


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

Et sous le capot : des virtual threads, donc aussi rapide qu’un code non bloquant*, mais beaucoup plus lisible.

\* c'est un point compliqué. En vrai, si je comprends bien:
- les threads classiques sont lents à créer, et lourds - au moins 1Mb par thread. C'est une grosse pénalité de la programmation concurrentielle.
- l'async et la programmation réactive sont conçus pour alléger cette pénalité : en évitant les attentes entre tâches confiées à chaque thread, en permettant que l'achèvement de l'une déclenche la suivante de façon fluide, et cela explicitement reflété dans l'expression du code. Les arrêts et pauses imposés par la gestion des threads (le "code bloquant") sont minimisées.
- mais les virtual threads réduisent quasiment à zéro la pénalité d'utiliser un pool réduit de threads lents à créer et lourds en mémoire. Il n'y a donc plus besoin d'avoir une approche dédiée à débloquer ou fluidifier cette gestion de threads. Cest en ce sens que les virtual threads sont "non bloquants".

Avec cette nouvelle approche, on peut utiliser la concurrence sans devoir faire des numéros d’équilibriste :

* Est-ce que la tâche va créer des milliers de sous-tâches ?
* Si oui, ces tâches vont elles être gourmandes ? Quel Executor choisir ?  Combien de threads faut-il prévoir ?
* Comment gérer les blocages et attentes qui resulteraient de l'assignation de mes (potentiellement) milliers de tâches à un pool de quelques dizaines de threads ?

On peut y aller beaucoup plus en confiance : démarrer des tâches, les superviser, attendre leur résultat, sans que le coût caché (en termes de gestion de threads) explose derrière.

# Où en est la Structured Concurrency aujourd'hui ?

La Structured Concurrency est arrivée en preview avec Java 21.

À fin avril 2025, elle est toujours en preview (avec quelques ajustements mineurs) dans Java 24.

Elle devrait être stabilisée et devenir officielle prochainement — mais elle est déjà totalement utilisable pour les projets qui ciblent un JDK récent.

# A propos
Je suis Clément Levallois, universitaire et développeur indépendant de [nocode functions](https://nocodefunctions.com) 🔎, une application d'analyse de rexte et de réseaux. Cette app est [open source](https://github.com/seinecle/nocodefunctions).

- **Email:** [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com) 📧  
- **Bluesky:** [@seinecle](https://bsky.app/profile/seinecle.bsky.social) 📱  
- **Blog:** [Plus d'articles](https://nocodefunctions.com/blog) 👓.
