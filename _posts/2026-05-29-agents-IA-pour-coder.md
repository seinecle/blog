---
layout: post
title: "Trois manières de coder avec des agents IA"
permalink: /coder-avec-agents-IA/
published: true
date_readable: May 29, 2026
last_modified_at_readable: May 29, 2026
categories: [ia,productivité,coding,développement,agentic,agentique]
---------------------------------------------------------------

Une définition raisonnable d’un « agent IA », au moins dans le contexte du codage agentique, pourrait être la suivante :

* un processus logiciel doté des capacités d’un LLM
* lancé avec des instructions données au départ pour accomplir une tâche
* qui s’exécute de manière autonome (pas de session interactive avec un humain), pendant une période significative
* avec un comportement non déterministe : l’agent s’adapte aux circonstances, si possible sans s’écarter des instructions qu’il a reçues

Ces processus logiciels (agents) peuvent être lancés en parallèle afin d’obtenir des résultats plus rapidement ou d’accomplir un plus grand nombre de tâches : le même processus lancé en plusieurs exemplaires, ou bien une variété de processus lancés en même temps.

Pour accomplir une tâche, un processus peut être amené à lancer d’autres processus, des sous-processus, etc.
Cela évoque des images de cascades, d’armées ou d’essaims d’agents qui se coordonnent de manière décentralisée (sans humain dans la boucle) pour accomplir une tâche.

Pourtant, en pratique, le terme « agents » est souvent utilisé sans rapport avec la définition ci-dessus.
Peut-être pour paraître à jour et sophistiqué, « agents » peut en réalité désigner une simple conversation ChatGPT dans laquelle l’utilisateur a écrit, par exemple : « tu agis comme un **agent** fiscal professionnel et, dans ce qui suit, je veux que tu m’aides à remplir ma déclaration d’impôts » 🤷‍♂️.

Pieter Levels, qui a tendance à parler franchement de code et d’IA, partageait ce sentiment à l’été 2025 :

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">If I hear people talk about &quot;AI agents&quot; these days it&#39;s generally a red flag and I know they&#39;re non-technical ppl reading AI news but not actually shipping anything<br><br>Not cause I don&#39;t believe in AI agents but it&#39;s such a marketing term with no real meaning at this point</p>&mdash; @levelsio (@levelsio) <a href="https://x.com/levelsio/status/1953125500492128766?ref_src=twsrc%5Etfw">August 6, 2025</a></blockquote>

**Nous approchons maintenant de l’été 2026 : les choses ont-elles beaucoup changé ?**

Dans ma pratique du code, j’ai exploré plusieurs façons de faire du codage agentique qui correspondent vraiment à la définition proposée ci-dessus, plutôt que de simplement en donner l’apparence.

Voici les 3 approches que j’ai testées :

# Approche 1 : lancer plusieurs interfaces en ligne de commande

J'ai pratiqué cette approche pendant quelques mois :

* ouvrir une session SSH vers mon serveur
* lancer [Codex CLI](https://developers.openai.com/codex/cli) dans cette session
* demander à GPT d’accomplir une tâche, pour cela j'écris simplement un prompt qui décrit cette tâche
* ouvrir une deuxième session SSH vers mon serveur
* lancer [Codex CLI](https://developers.openai.com/codex/cli) dans cette session
* demander à GPT d’accomplir une autre tâche, pour cela j'écris simplement un prompt qui décrit cette tâche
* et ce processus peut se répèter à l'infini 

Honnêtement, cela fonctionne assez bien.
C’est extrêmement low-tech, comme vous pouvez le voir.
Cela signifie aussi que vous pouvez lancer [Claude Code](https://claude.com/fr/product/claude-code) dans une session, Codex CLI dans une autre, [Gemini CLI](https://geminicli.com/) dans une troisième... et donc répartir votre consommation de tokens entre plusieurs fournisseurs d’IA en parallèle, ce qui fait qu'on atteint moins vite sa limite de budget en tokens chez un fournisseur donné.

# Approche 2 : lancer des CLI IA en mode headless
J’ai utilisé cette deuxième approche pour écrire des crawlers pour plus de 200 pages web différentes.
Évidemment, avec 200 crawlers à créer, cela aurait été beaucoup trop ennuyeux à faire avec l’approche 1 décrite juste au-dessus.
ChatGPT m’a guidé tout au long de la mise en œuvre de cette nouvelle approche. La logique de base est la suivante :

* un fichier JSON contenant les paramètres des 200 sites web (URLs et quelques autres détails).
* un script Bash (appelons-le « A ») capable de lancer un LLM via une interface en ligne de commande, en mode headless. Headless signifie que le LLM, une fois lancé avec le prompt que vous lui avez donné, s’exécutera jusqu’à ce qu’il ait terminé la tâche, sans s’interrompre pour vous demander une permission, un retour ou une suite. Pour cela, j’utilise le [`flag exec` de Codex CLI qui déclenche le mode headless](https://developers.openai.com/codex/noninteractive). Le script A contient également le prompt qui sera donné au LLM au moment de son lancement. Le prompt est un morceau de texte avec des placeholders à des endroits clés, qui sont remplacés par les informations réelles liées au site web spécifique à crawler. Le prompt demande essentiellement au LLM d’écrire un crawler pour ce site web.
* un autre script (le script « B ») qui prend 20 sites web dans le fichier JSON et exécute le script A pour chacun d’eux. Les placeholders du script A sont remplacés par les informations du site web à crawler, ce qui signifie que le crawler créé par le LLM sera spécifique à ce site web.
* je lance le script B, je vérifie qu’il fonctionne correctement, puis je le relance avec 20 autres sites web, etc., jusqu’à avoir traité 200 sites web de cette manière.

Je vous montre le script A (script écrit par ChatGPT) pour illustrer en quoi cette approche 2 implique bien plus de complexité que l’approche 1 :

<details>
<summary><strong>Long script A — click to expand</strong></summary>

```
#!/usr/bin/env bash
set -euo pipefail

ROOT="/home/xxx/backend"

PACKAGE="${1:?missing package}"
SOURCE_ID="${2:?missing source_id}"
PLATFORM="${3:?missing platform}"
URL="${4:?missing url}"
LOCAL_GUARDRAIL="${CODEX_LOCAL_GUARDRAIL:-1}"

PROMPT="$ROOT/ops/codex/prompts/${PACKAGE}-agent.txt"
LOG_MD="$ROOT/reports/codex/logs/${PACKAGE}-agent.md"
STDOUT_LOG="$ROOT/reports/codex/logs/${PACKAGE}-stdout.log"
STDERR_LOG="$ROOT/reports/codex/logs/${PACKAGE}-stderr.log"

echo "[$(date -Is)] preparing ${PACKAGE}"

cat > "$PROMPT" <<EOF
You are source_crawler_creator.

Create or repair exactly one isolated direct-site crawler package.

SOURCE_ID: ${SOURCE_ID}
URL: ${URL}
PLATFORM: ${PLATFORM}
PACKAGE_NAME: ${PACKAGE}
PACKAGE_PATH: src/main/java/com/xxx/directsite/crawling/sources/${PACKAGE}

Writable paths:
- src/main/java/com/xxx/directsite/crawling/sources/${PACKAGE}/**
- src/test/java/com/xxx/directsite/crawling/sources/${PACKAGE}/**
- src/test/resources/directsite/${PACKAGE}/**
- reports/codex/source-results/${PACKAGE}.json
- reports/codex/shared-change-requests/${PACKAGE}.md

Read-only reference paths:
- src/main/java/com/xxx/directsite/crawling/sources/estia/**
- src/main/java/com/xxx/directsite/crawling/sources/groupeesa/**
- src/main/java/com/xxx/directsite/crawling/sources/generic/**
- src/main/java/com/xxx/directsite/crawling/sources/ats/**
- src/main/java/com/xxx/directsite/crawling/sources/talentsoft/**
- src/main/java/com/xxx/directsite/crawling/rules/**
- src/main/java/com/xxx/directsite/crawling/CrawlerRegistry.java
- src/main/java/com/xxx/directsite/crawling/DirectSiteCrawler.java
- src/main/java/com/xxx/directsite/crawling/DirectSiteCrawlerSupport.java
- src/main/java/com/xxx/directsite/crawling/sources/AGENTS.md
- AGENTS.md
- pom.xml

Hard constraints:
- Modify only the writable paths listed above.
- Do not edit CrawlerRegistry.java.
- Do not edit shared crawler classes, including ats and talentsoft reference packages.
- Do not edit shared pipeline, shared DTOs, pom.xml, or AGENTS.md.
- Do not touch any other source package.
- If registration is required in shared code, do not make that shared change. Report it.
- Keep crawl, parse, reconcile, and LLM enrichment concerns separate.
- For platform-specific sources, inspect the existing platform package as a read-only reference and create only source-specific wrappers/specs if useful.

Testing rules:
- JUnit tests must not perform live network calls.
- Use local fixtures under src/test/resources/directsite/${PACKAGE}/ for detail HTML whenever practical.
- Inline HTML/JSON is acceptable only for very small snippets.
- Prefer behavior assertions over brittle exact cardinality unless the fixture is intentionally constructed for that cardinality.
- Do not assert overly specific live data fields unless they are necessary to lock parser behavior.
- If asserting URLs/titles from fixtures, treat them as fixture examples, not as proof that the live page still exists.

Task:
1. Inspect existing crawler patterns.
2. Investigate the URL and determine xxx.
3. Create or repair the dedicated ${PACKAGE} crawler package.
4. Implement only source-specific crawling/parsing details in this package.
5. Reuse shared rules/classes when applicable.
6. Add narrow tests if practical.
7. Run the narrowest useful Maven compile/test command.
8. Write reports/codex/source-results/${PACKAGE}.json with:
{
  "source_id": "${SOURCE_ID}",
  "package": "${PACKAGE}",
  "status": "created|repaired|blocked|needs_shared_change",
  "files_changed": [],
  "tests_run": [],
  "shared_change_requested": false,
  "notes": "..."
}

Final answer:
- concise summary
- files changed
- tests run
- whether shared change is needed
EOF

echo "[$(date -Is)] starting ${PACKAGE}"

if [ "$LOCAL_GUARDRAIL" = "1" ]; then
  BEFORE_STATUS="$(mktemp)"
  AFTER_STATUS="$(mktemp)"
  git status --short --untracked-files=all > "$BEFORE_STATUS"
fi

codex exec \
  --cd "$ROOT" \
  --sandbox workspace-write \
  --model gpt-5.4 \
  --output-last-message "$LOG_MD" \
  - < "$PROMPT" \
  > "$STDOUT_LOG" \
  2> "$STDERR_LOG"

if [ "$LOCAL_GUARDRAIL" = "1" ]; then
  git status --short --untracked-files=all > "$AFTER_STATUS"

  FORBIDDEN="$(
    comm -13 <(sort "$BEFORE_STATUS") <(sort "$AFTER_STATUS") \
      | cut -c4- \
      | grep -vE "^(\.codex/|ops/codex/|reports/codex/|src/main/java/com/xxx/directsite/crawling/sources/${PACKAGE}/|src/test/java/com/xxx/directsite/crawling/sources/${PACKAGE}/|src/test/resources/directsite/${PACKAGE}/)" || true
)"
    if [ -n "$FORBIDDEN" ]; then
      echo "[$(date -Is)] FORBIDDEN FILE CHANGES for ${PACKAGE}:" >&2
      echo "$FORBIDDEN" >&2
      exit 42
    fi
fi
echo "[$(date -Is)] finished ${PACKAGE}"
```

</details>

Cette approche fonctionne bien.
Ce n’est pas aussi simple que « lancer le script A et obtenir 200 crawlers écrits en une heure », mais on n’en est pas si loin.
Si vous avez la patience de lire un peu le script ci-dessus, vous verrez que le LLM a aussi pour tâche d’écrire des tests unitaires pour chaque crawler qu’il crée !
Comme on peut s’y attendre, ces tests ne passent pas toujours, ce qui ralentit un peu les choses.
Mais c’est pour une bonne raison : faire le travail supplémentaire nécessaire pour obtenir des tests qui passent signifie que les crawlers seront plus fiables.

Avec cette approche, je m’attends à avoir mes 200 crawlers prêts dans les prochains jours, avec un chemin assez simple pour monter ensuite à plusieurs centaines de plus.

# Approche 3 : demander à un LLM de créer et de gérer lui-même ces sous-agents

L’approche 2 était vraiment très orientée Bash et Unix : ca demande du travail de maintenance de scripts.
Pourquoi ne pas demander à un LLM de lancer lui-même des agents, en suivant mes instructions ?
C’est ce que toutes les solutions promettent aujourd’hui :

* Cursor vous invite à ["déléguer l'implémentation pour se concentrer sur la direction de haut niveau"](https://web.archive.org/web/20260528201253/https://cursor.com/product)
* Codex propose des ["sub-agents"](https://web.archive.org/web/20260524042439/https://developers.openai.com/codex/subagents) que vous pouvez orchestrer
* Antigravity de Google propose d'["orchestrer de multiples agents autonomes travaillant en parallèle sur des projets indépendants"](https://perma.cc/4S83-LRM3)
* Claude Code peut créer des ["sous-agents personnalisés"](https://web.archive.org/web/20260528082943/https://code.claude.com/docs/en/sub-agents) pour vous.

Mon avis : probablement, mais pas aujourd’hui.
Demander à un agent de déléguer à des sous-agents signifie que vous êtes à deux niveaux de distance du travail réel.
Les incohérences, les mauvais choix, les erreurs critiques ... seront plus difficiles à repérer.
L’interruption puis la reprise du travail d’un sous-agent donné ne sont pas simples.
Et vous devenez dépendant d’une solution : mon IA de prédilection ces temps-ci est GPT 5.5, et elle serait hors limites si je choisissais une solution agentique qui n’est pas développée par son entreprise, OpenAI.

> Pour ces raisons, et jusqu’à preuve du contraire, je vais m’en tenir à l’approche 2 (et même à l’approche 1 dans les cas simples) décrite ci-dessus.

# Avons-nous vraiment besoin d’agents ?

La plupart du temps, *non*.
Voici [Ethan Mollick](https://www.linkedin.com/in/emollick/) en train de créer une application web complète et fonctionnelle avec un seul prompt et 4 relances, pour un total de moins de 20 lignes :

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">How lucky are you to have been born when and where you are?<br><br>Had Opus 4.8 in Claude Code whip up a new visualization of all humans who ever lived. In addition to being neat, it is an interesting test of combining research, code, design and stats for an AI. <a href="https://t.co/ayNEdhSLy3">https://t.co/ayNEdhSLy3</a> <a href="https://t.co/Ny2NmICZsK">pic.twitter.com/Ny2NmICZsK</a></p>&mdash; Ethan Mollick (@emollick) <a href="https://x.com/emollick/status/2060165879908749490?ref_src=twsrc%5Etfw">May 29, 2026</a></blockquote>

Il n'a pas eu besoin de développer une approche agentique, les prompts ont suffit.

Un autre exemple est le site développé par ma fille : une [plateforme e-commerce complète](https://www.daebias.com/).
Développée sans technologie sophistiquée ni échafaudage agentique. Juste des prompts (et beaucoup de travail).

Vous avez probablement aussi remarqué que, dans les conversations avec des LLMs où nous leur demandons de chercher de l’information, ces LLMs peuvent choisir de lancer des recherches sur différents sites web, chaque recherche étant effectuée par son propre agent.
Cela les aide à accélérer leur recherche et à couvrir davantage de terrain en réponse à votre demande.

Je dirais donc que, dans la plupart des cas, nous n’avons pas besoin d’agents, même pour des tâches complexes, parce que les LLMs fonctionnent très bien sans eux.
Et si des agents sont utiles, alors les LLMs lancent leurs propres agents et les gèrent sous le capot.

# Cerise sur le gâteau : les agents qui se marchent sur les pieds

Le sujet est peu glamour et ce billet est déjà trop long, donc je serai bref : plusieurs agents qui écrivent simultanément dans votre codebase vont se marcher sur les pieds.
S’ils modifient le même fichier, il y a de fortes chances que le fichier résultant soit un désastre.

Le remède consiste à faire travailler chaque agent sur une [branche git](https://www.w3schools.com/GIT/git_branch.asp) différente, puis à procéder à un *merge* de ces branches dans la branche principale une fois que tous les agents ont terminé.
C’est aussi un bazar : que se passe-t-il si le *merge* échoue ? (et bien sûr, il échouera).
J’ai essayé cette approche, et elle est fastidieuse, crispante, et vous donne vite envie d’abandonner l'approche multi-agent.

Alors comment ai-je fait, dans l’approche 2, pour créer des dizaines de crawlers sans que les agents ne se rentrent dedans ?

J’ai d’abord mené un important travail préparatoire sur un seul crawler, en m’assurant qu’il fonctionnait en parfaite isolation par rapport aux autres.
Ce n’est pas une tâche facile quand on veut malgré tout suivre le principe DRY (*don’t repeat yourself*) en programmation.
Ce n’est qu’à la condition que chaque crawler soit parfaitement isolé que vous pouvez faire travailler simultanément des dizaines d’agents sur des fichiers source sans créer de désastre.

Si vous remontez et regardez le script Bash que j’ai partagé, vous verrez que ChatGPT m’a également conseillé sur ce point, en ajoutant des blocages stricts dans le prompt, de sorte que chaque agent se voit explicitement interdire de toucher aux fichiers qui ne sont pas dans le périmètre de son travail.

# Prochaines étapes

Passer de dizaines de crawlers écrits avec l’approche 2 à des centaines de crawlers.
Puis les exécuter.
Devenir suffisamment compétent dans ce setup multi-agent « fait maison » pour pouvoir le reproduire ailleurs, quand et si j’en ai besoin.

# Et vous ?

Quel setup multi-agent fonctionne pour vous ? Ou bien restez-vous sans agent ?

---

# À propos de moi

Je suis universitaire et développeur indépendant d’applications web. J’ai créé [nocode functions](https://nocodefunctions.com), un outil point-and-click pour explorer des textes et des réseaux. Essayez-le et dites-moi ce que vous en pensez. Vos retours m’intéressent beaucoup !

* **Email :** [analysis@exploreyourdata.com](mailto:analysis@exploreyourdata.com)
* **Bluesky :** [@seinecle](https://bsky.app/profile/seinecle.bsky.social)
* **Blog :** [Lire d’autres articles](https://nocodefunctions.com/blog) sur le développement d’applications et l’exploration de données.
