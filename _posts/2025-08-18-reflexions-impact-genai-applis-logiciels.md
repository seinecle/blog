---

layout: post
title: "Réflexions sur l'impact de l'IA générative sur les applications logiciels"
permalink: /réflexions-ia-generative-applications-logiciels/
published: true
date\_readable: 18 August 2025
last\_modified\_at\_readable: 18 August 2025
categories: \[IA, IA générative, applications logiciels, destruction créatrice, french]
---

Ce sont des notes personnelles sur la manière dont l’IA générative impacte les applications logicielles. Ce post est traduit [de l'anglais](/blog/more-thoughts-on-impacts-of-genAI-on-software-applications/) et fait suite à [ce post précédent, en anglais aussi](/blog/three-impacts-of-genAI-on-software-applications/).

# Ce que l’IA générative *peut* faire en août 2025

## 1. Prendre des fichiers multimodaux en entrée

Jusqu’à l’année dernière, la plupart des applis d’IA générative étaient limitées quant aux types de fichiers qu’elles pouvaient lire.
Gemini ne pouvait même pas lire les PDF si je me souviens bien.
Cette barrière est tombée.

La plupart des applis acceptent désormais txt, csv, pdf, docx, xlsx, pptx, tout xml ou json.
Plus important encore, toutes les grandes applis d’IA générative sont désormais multimodales : elles acceptent du texte mais aussi des images en entrée et peuvent en faire des analyses de contenu très détaillées.
J’ai testé avec Le Chat de Mistral (version gratuite), Gemini, Claude (version gratuite) et ChatGPT : toutes ont pu décrire une capture d’écran de mon ordinateur avec un grand niveau de précision.

L’analyse sonore est arrivée aussi. On peut réaliser une analyse détaillée d’un fichier .wav, par exemple (en août 2025, seul ChatGPT possède cette capacité).

Et la vidéo ? Pour l’instant, seul ChatGPT peut traiter des vidéos : sur la vidéo que j’ai testée, il extrait un échantillon d’images puis tente d’en déduire un sens.

## 2. Réaliser des analyses avancées, à la volée

ChatGPT peut désormais lancer un mini environnement informatique pour traiter vos requêtes à la volée : il peut exécuter n’importe quel code Python disponible librement en bibliothèque packagée sur le web.

## 3. Raisonnement

La capacité de raisonnement est ce qui a fait le succès de l'IA générative : l’effet saisissant des LLMs est qu’ils (semblent) raisonner comme le ferait un humain.
À vous d’apprécier si cet humain correspond à « un stagiaire », « un étudiant » ou « un niveau doctorat », mais cela reste assez proche de ce qu’un humain ferait.

Le raisonnement a pris une nouvelle tournure depuis l’automne 2024 ([OpenAI](https://openai.com/fr-FR/index/introducing-openai-o1-preview/)) / février 2025 ([Claude](https://www.anthropic.com/news/claude-3-7-sonnet)) / mars 2025 ([Gemini](https://blog.google/technology/google-deepmind/gemini-model-thinking-updates-march-2025/#gemini-2-5-thinking)) avec la capacité pour une IA générative d’itérer : elle peut désormais se nourrir de ses propres résultats, ce qui permet réexamens, modifications et améliorations avant que la version finale ne soit livrée à l’utilisateur.

### Générer du contenu interactif

Tous les grands fournisseurs savent désormais générer des images et des applications web interactives.

# Ce que l’IA générative *ne peut pas* faire en août 2025

## ~~1. Se connecter à des sources de données "live"~~

Analyser les données de Bluesky, Reddit ou LinkedIn en direct ?
C’est probablement déjà possible : après tout, j’imagine qu’on peut fournir ses identifiants API pour l’un de ces services dans un prompt et cela permettrait à l’appli d’IA générative d’aller chercher les données pour vous.
*Mais ce n’est ni pratique ni direct*. Quid de la vitesse, des limites de mémoire, du contrôle fin, de la gestion d’erreurs et de la persistance des données collectées ?

J’étais sur le point de conclure ainsi, mais… Claude d’Anthropic contredit cet argument : depuis [mai 2025](https://www.anthropic.com/news/integrations) et avec des enrichissements fréquents depuis, il offre 2 types de connecteurs :

* connecteurs vers vos applis de bureau (navigateur, explorateur de fichiers, …),
* connecteurs vers des sources et services web (Canva, Gmail, Notion, etc.).

Ces connecteurs signifient que vous pouvez utiliser Claude pour raisonner et créer à partir de n’importe quel contenu produit sur votre ordinateur.

## 2. Gestion fine de l’information

Une IA générative conversationnelle peut désormais couvrir toute la chaîne du traitement de données :

* vous pouvez fournir divers inputs : fichiers, images, prompts
* ces inputs peuvent déclencher le lancement de diverses actions pour compléter la requête : recherche web, création d’un mini environnement informatique pour l’analytique, mode raisonnement, création de visuels, ou juste une réponse écrite rapide si c’est suffisant.
* vous pouvez ensuite sauvegarder le résultat : copier dans le presse-papiers, télécharger en fichier, ou télécharger l’image.

-> vous ne quittez jamais l’appli, tout est intégré.

**<u>Pourtant en pratique, malgré tout cela</u>, les tâches que nous effectuons nécessitent vite des manipulations élémentaires de données indisponibles dans l’environnement ChatGPT :**

-> recherche, filtrage, tri, renommage, mise en forme, fonction « annuler la dernière modification », …

Ces tâches sont perçues comme si élémentaires qu’elles en deviennent invisibles, situées à la périphérie de la proposition de valeur de tout logiciel.
Pourtant, elles sont la raison pour laquelle nous quittons une conversation ChatGPT et revenons à une application classique de bureau. Parce que « c’est plus simple et plus rapide » de les y faire.

Exemple : ChatGPT génère du texte, certes. Et il peut le mettre en forme grâce à [markdown](https://daringfireball.net/projects/markdown/), oui. Pourtant nous copions-collons le résultat dans Word puis passons du temps à peaufiner la mise en page.
Si la destination finale du texte est un PowerPoint, les étapes de reformatage sont encore plus lourdes.

## 3. Offrir des interfaces adaptées à la tâche

Argument assez évident : ChatGPT (et Claude, Gemini, etc.) sont des applis généralistes centrées sur une interface conversationnelle.
Cette interface n’est clairement *pas* la plus utile dans de nombreuses situations :

* besoin de manipuler des données tabulaires ? Une interface type Excel est essentielle
* vous êtes codeur ? Alors un IDE (environnement de développement intégré) est la solution éprouvée depuis des décennies
* vous êtes designer UX ? Alors une interface en canevas est nécessaire
* etc.

Les immenses ressources des acteurs clés de l’IA générative (Google, OpenAI, Anthropic – et Mistral ?) laissent penser qu’ils développeront ces types d’interfaces manquantes. Des interfaces « canvas » et « coding » ont déjà été ajoutées (voir ci-dessous), même si de façon rudimentaire. Mais faut-il souhaiter une appli « tout-en-un » ? La différenciation des logiciels en applis de bureau distinctes a eu lieu pour une raison : elle offre des choix de conception plus fins. Maintenir ce degré de différenciation dans une seule grosse « appli IA générative » semble difficile.

# 3 directions où ces tensions poussent l’innovation

## 1. L’évolution de l’interface chatbot

[OpenAI a lancé « Canvas » en 2024](https://openai.com/fr-FR/index/introducing-canvas/), une fenêtre qui s’ouvre à côté de la conversation lorsque l’information nécessite manifestement une autre forme d’affichage. Canvas peut prendre la forme d’un tableau, d’un éditeur de code, et peut produire et afficher tout ce qui peut être représenté comme une page web : applis, cartes, tableaux, etc.

-> [En mai 2025](https://blog.google/products/gemini/gemini-collaboration-features/), Gemini de Google a lancé une fonctionnalité similaire, également nommée « Canvas ».

Mon expérience : ce sont des fonctions « sympa à avoir » mais pas encore très utiles. Passés les cas simples, le rendu HTML est buggé et des fonctionnalités avancées manquent immédiatement (pour les données tabulaires notamment).

Je suis curieux de voir la suite : ces interfaces diversifiées dans l’appli IA générative visent-elles les utilisateurs « intermédiaires », qui n’ont pas besoin de la pleine puissance d’une appli complète ? Ou ciblent-elles aussi les utilisateurs avancés, pour leurs besoins de prototypage rapide avant de basculer sur des applis de bureau ? Ou encore, ces entreprises croient-elles vraiment qu’elles offriront la même expérience que les applis de bureau – ChatGPT remplaçant un jour Figma ? Ce dernier scénario me paraît improbable.

## 2. La montée de l’IA intégrée

C’est a priori un mouvement malin : les logiciels existants ont tout le confort d’une interface familière, spécialisée, auprès d’une large base d’utilisateurs. Il suffit d’y ajouter des capacités IA (analyse, raisonnement) et le tour est joué. Pensez à Microsoft Copilot dans Excel. Mais à ce jour, mon expérience personnelle est très décevante :

* Copilot dans Excel n’apporte rien d’utile : il réussit des tâches simples, que vous auriez faites plus vite vous-même (ajouter une colonne qui somme deux autres colonnes). Mais il échoue sur les tâches plus complexes, comme le formatage d’un tableau ou le remplissage de valeurs avec une formule avancée.
* Autre exemple (anecdotique) : l’appli que j’utilise pour les courses. Ils ont introduit une fonction « IA générative » censée préremplir mon panier selon mes achats précédents. Échec total : un simple système expert aurait suffi (« suggérer les produits les plus fréquemment/récemment achetés »).

Un domaine bien plus réussi est celui des environnements de développement intégrés (IDE) : ces logiciels offrent aux programmeurs tous les outils pour coder plus vite et plus confortablement (automatisation des tâches répétitives, etc.).

Aujourd’hui, tous les grands IDE proposent du code assisté par IA. Les développeurs les utilisent activement, au point que l’absence de ces fonctions est vécue comme un frein à la productivité. Exemples : [JetBrains](https://www.jetbrains.com/help/idea/ai-assistant-in-jetbrains-ides.html) ou [VS Code](https://www.infoworld.com/article/3982310/visual-studio-code-beefs-up-ai-coding-features.html?utm_source=chatgpt.com).

Mon impression générale : après une période (peut-être longue) d’expériences décevantes et de promesses gonflées (« notre appli est désormais IA powered ! – pas vraiment »), les choses s’amélioreront peu à peu et les applis de bureau garderont leur pertinence. Parce que les applis d’IA générative ne peuvent pas tout absorber sans devenir gonflées et limitées (cf. plus haut), les logiciels établis peuvent prospérer.

## 3. L’émergence d’applis natives IA

C’est un champ de développement très actif, je ne serai pas exhaustif. Trois exemples :

* [Scenario](https://www.scenario.com/) qui génère des assets 3D.
* [Shortcut](https://www.tryshortcut.ai/) qui est comme Excel, mais avec IA intégrée.
* [Suno](https://suno.com/home) qui génère de la musique.

À retenir sur ces logiciels :

1. Les premiers retours suggèrent qu’ils améliorent considérablement la productivité des pros dans certaines tâches clés de leur domaine. Voir pour [Scenario](https://x.com/emmanuel_2m/status/1947372337529004253), [Shortcut](https://x.com/nicochristie/status/1949862432077484396) et [Suno](https://x.com/levelsio/status/1957155181591777503).
2. Pour Scenario et Suno, liés à la création artistique, on peut prévoir des débats épineux sur la qualité de leurs outputs. Moins vrai pour Shortcut, plus orienté bureautique.
3. Les entreprises adopteront ces outils dès qu’elles constateront un vrai gain de productivité.
4. Trois segments émergeront :
   * production de masse et à bas coût d’assets culturels **entièrement produits par IA** (pubs, musique d’ascenseur, centres commerciaux, etc.)
   * artefacts culturels « artistiques », en petites séries, « faits main », **sans IA générative**. Objets de luxe pour marchés haut de gamme mais aussi productions d’artistes locaux sur des scènes indépendantes.
   * industries créatives produisant films, expériences et événements **avec un mix d’IA générative et de logiciels traditionnels** (ex : Blender).

Mon point de vue :
Ces trois exemples pourraient laisser penser que c’est une voie garantie vers le succès. **Absolument pas** : ces logiciels risquent d’être supplantés, totalement remplacés par les progrès des applis généralistes comme ChatGPT, Claude, Gemini (et Le Chat ?). Quelques exemples :

*Nés avec la vague IA générative :*

* [Otter.ai](https://otter.ai/) : transcription de réunions vidéo
* [photoai.com](https://photoai.com/) : génération de shootings photo à partir d’échantillons

*Nés avant la vague IA générative :*

* [Grammarly](https://www.grammarly.com/) : correction et amélioration stylistique de texte
* [DeepL](https://www.deepl.com/fr/translator) : traduction

Ces 4 services sont menacés d’obsolescence car on peut obtenir le même service gratuitement via ChatGPT ou équivalents. Par exemple, je viens de traduire cet article de blog de l'anglais vers le français avec un simple prompt...

Dit autrement, comme le montre un mème populaire : un simple prompt ChatGPT peut donner le même résultat qu’une appli dédiée, la rendant inutile :

![https://medium.com/@msgforrobin/become-a-chatgpt-pro-in-5-minutes-the-only-prompt-youll-ever-need-3b094bb27e8f](https://github.com/user-attachments/assets/96a3b04b-e250-4d03-8134-0691a2a765e4)

Il est intéressant de voir les réactions et stratégies de ces services pour survivre : comme évoqué plus haut, il leur reste à offrir un contrôle plus fin et nuancé de l’information et des paramètres, afin de se différencier d’une simple conversation ChatGPT. À mes yeux, seul photoai.com réussit cette stratégie pour l’instant.

Les entrepreneurs lançant des services natifs IA ont donc une tâche redoutable : anticiper les capacités de l’IA générative d’ici 2 à 5 ans et s’assurer que leur service **aujourd’hui** ne sera pas rendu obsolète par ces capacités demain. Pari excitant, mais risqué !

---

# À propos de moi

Je suis enseignant-chercheur et développeur indépendant d’applications web. J’ai créé [nocode functions](https://nocodefunctions.com) 🔎, un outil gratuit en point-and-click pour explorer textes et réseaux. C’est [entièrement open source](https://github.com/seinecle/nocodefunctions). Essayez-le et dites-moi ce que vous en pensez. Vos retours m’intéressent !

* **Email :** [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com) 📧
* **Bluesky :** [@seinecle](https://bsky.app/profile/seinecle.bsky.social) 📱
* **Blog :** [Lire d’autres articles](https://nocodefunctions.com/blog) 👓 sur le développement d’applications et l’exploration de données.
