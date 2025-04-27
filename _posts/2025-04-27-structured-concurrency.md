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
