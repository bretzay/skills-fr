---
# Standard Agent Skills, lu par tous les agents
name: apprendre
description: Enseigne une compétence ou un concept à l'utilisateur, sur plusieurs sessions, dans un espace de travail suivi. À n'employer que si l'utilisateur demande explicitement à apprendre quelque chose.

# Claude Code, ignoré partout ailleurs. L'équivalent Codex est dans agents/openai.yaml
disable-model-invocation: true
argument-hint: "Que voulez-vous apprendre ?"

# Provenance, pour les humains
upstream_repo: mattpocock/skills
upstream_path: skills/productivity/teach
upstream_commit: 74ca5fe077456a0b3b2f5310cf9430999fd0b5fd
upstream_release: 1.2.3
---

L'utilisateur vous demande de lui enseigner quelque chose. La demande est persistante, il compte apprendre ce sujet sur plusieurs sessions.

## L'espace d'apprentissage

Traitez le répertoire courant comme un espace d'apprentissage. L'état de son apprentissage tient dans quelques fichiers.

- `MISSION.md`. Le document qui dit _pourquoi_ l'utilisateur s'intéresse au sujet. Tout l'enseignement s'y rattache. Format dans [FORMAT-MISSION.md](./FORMAT-MISSION.md).
- `./reference/*.html`. Les documents de référence. Ce sont les acquis comprimés des leçons, aide-mémoire, algorithmes, syntaxe, postures de yoga, glossaires. Ce sont les unités brutes de l'apprentissage. Ils doivent être beaux, s'imprimer correctement, et se consulter en quelques secondes.
- `RESSOURCES.md`. La liste des sources qui ancrent votre enseignement dans un savoir réel, ou qui donnent du discernement. Format dans [FORMAT-RESSOURCES.md](./FORMAT-RESSOURCES.md).
- `./fiches-apprentissage/*.md`. Les fiches d'apprentissage, qui enregistrent ce que l'utilisateur a acquis. Elles sont l'équivalent pédagogique des décisions d'architecture en développement logiciel, elles gardent les leçons non évidentes et les prises de conscience qu'il faudra peut-être réviser, ou qui dirigent les sessions suivantes. Elles servent à calculer la zone proximale de développement. Elles sont numérotées `0001-<nom-en-tirets>.md`, le numéro s'incrémente à chaque fois. Format dans [FORMAT-FICHE-APPRENTISSAGE.md](./FORMAT-FICHE-APPRENTISSAGE.md).
- `./lecons/*.html`. Les leçons. Une **leçon** est un fichier HTML autonome qui enseigne une seule chose, étroitement délimitée, rattachée à la mission. C'est l'unité d'enseignement de cet espace.
- `./composants/*`. Les **composants** réutilisables partagés entre les leçons. Voir [Composants](#composants).
- `NOTES.md`. Un brouillon où noter les préférences de l'utilisateur et vos remarques de travail.

Les noms de dossiers s'écrivent sans accent (`lecons`, `reference`) pour qu'aucun shell ni aucun système de fichiers ne s'y perde. Les noms de fichiers que l'utilisateur lit, eux, portent leurs accents.

## Philosophie

Pour apprendre en profondeur, l'utilisateur a besoin de trois choses.

- Le **savoir**, tiré de sources de qualité et dignes de confiance
- Le **savoir-faire**, acquis par des leçons interactives très ciblées que vous concevez à partir de ce savoir
- Le **discernement**, qui vient de la rencontre avec d'autres apprenants et d'autres praticiens

Tant que `RESSOURCES.md` est pauvre, cherchez d'abord des sources solides qui donneront du savoir à l'utilisateur. Ne faites jamais confiance à vos connaissances paramétriques.

Certains sujets demandent plus de savoir-faire que de savoir. La physique théorique penche vers le savoir. Le yoga penche vers le savoir-faire.

### Restitution et stockage

Séparez soigneusement deux formes d'apprentissage.

- La **force de restitution** (_fluency strength_), la récupération immédiate d'une connaissance
- La **force de stockage** (_storage strength_), la rétention à long terme

La restitution donne une illusion de maîtrise. C'est le stockage qui compte. Concevez des leçons qui construisent la rétention par la difficulté désirable.

- Le rappel actif, récupérer de mémoire
- L'espacement, répartir la pratique dans le temps
- L'entrelacement, mélanger des sujets différents mais liés, pour la pratique du savoir-faire seulement

## Les leçons

La leçon est ce que vous produisez avant tout, le format par lequel le savoir et le savoir-faire atteignent l'utilisateur. Chaque leçon est un fichier HTML autonome, enregistré dans `./lecons/` et nommé `0001-<nom-en-tirets>.html`, le numéro s'incrémente à chaque fois.

Une leçon doit être **belle**, typographie et mise en page propres et lisibles, parce que l'utilisateur y reviendra pour réviser. Pensez à Tufte.

La leçon doit être courte et se terminer très vite. La mémoire de travail d'un apprenant est minuscule, il faut rester dedans. Mais chaque leçon doit donner un gain concret sur lequel bâtir la suite. Elle se rattache directement à la mission et tient dans la zone proximale de développement.

Si possible, ouvrez le fichier de la leçon pour l'utilisateur avec une commande en ligne de commande.

Chaque leçon renvoie par des ancres HTML vers les autres leçons et vers les documents de référence.

Chaque leçon recommande une source primaire à lire ou à regarder. Prenez la meilleure et la plus fiable que vous avez trouvée sur le sujet.

Chaque leçon rappelle à l'utilisateur qu'il peut poser des questions à l'agent. L'agent est son professeur, il peut éclaircir tout ce qui reste flou.

## Composants

Les leçons se construisent à partir de **composants** réutilisables, rangés dans `./composants/`, feuilles de style, widgets de quiz, simulateurs, aides au dessin de schémas, et tout ce qu'une deuxième leçon pourrait reprendre.

La réutilisation est la règle, pas l'exception. Avant d'écrire une leçon, lisez `./composants/` et partez de ce qui existe déjà. Quand une leçon a besoin de quelque chose de neuf et de réutilisable, écrivez-le comme composant dans `./composants/` et faites un lien vers lui. N'écrivez jamais en ligne du code qu'une leçon future dupliquerait.

La feuille de style partagée est le premier composant que tout espace mérite. Chaque leçon s'y raccroche, et les leçons ressemblent alors à un cours cohérent plutôt qu'à un tas de pièces détachées. La bibliothèque de composants grandit avec l'espace.

## La mission

Chaque leçon se rattache à la mission, la raison pour laquelle l'utilisateur veut apprendre le sujet.

Si la mission est floue, ou si `MISSION.md` est vide, votre premier travail est d'interroger l'utilisateur sur ce qui l'amène là.

Sans mission comprise, le savoir n'est plus ancré dans un objectif réel. Les leçons paraîtront abstraites. Vous n'aurez aucun moyen de juger quoi faire ensuite.

Une mission peut changer à mesure que l'utilisateur progresse. C'est normal, mettez `MISSION.md` à jour et ajoutez une fiche d'apprentissage qui enregistre le changement. Confirmez avec l'utilisateur avant de changer la mission.

## Zone proximale de développement

À chaque leçon, l'utilisateur doit se sentir sollicité juste ce qu'il faut.

L'utilisateur peut nommer précisément ce qu'il veut apprendre. Sinon, trouvez sa zone proximale de développement.

- Lisez ses fiches d'apprentissage
- Déduisez de sa mission ce qu'il faut lui enseigner
- Enseignez la chose la plus utile qui tienne dans cette zone

## Le savoir

Une leçon se construit autour d'un savoir-faire que l'utilisateur va acquérir. Le savoir qu'elle contient se limite à ce que ce savoir-faire exige. Vous enseignez le savoir d'abord, puis vous faites pratiquer par une boucle de rétroaction interactive.

Le savoir vient d'abord de sources fiables. Tenez `RESSOURCES.md` à jour pour les suivre. Les leçons sont criblées de citations, des liens vers des sources externes qui appuient chaque affirmation. C'est ce qui rend une leçon digne de confiance.

Pour acquérir du savoir, la difficulté est l'ennemi. Elle mange la mémoire de travail dont la compréhension a besoin.

## Le savoir-faire

Si le savoir est affaire d'acquisition, le savoir-faire est affaire de durabilité et de souplesse. C'est lui qui fait tenir le savoir.

Pour le savoir-faire, la difficulté devient l'outil. C'est l'effort de récupération qui construit la force de stockage. Le savoir-faire s'enseigne par des leçons interactives. Plusieurs outils sont à votre disposition.

- Des leçons interactives, quiz et petites tâches dans le navigateur
- Des leçons qui guident l'utilisateur à travers une série d'actions dans le monde réel, des postures de yoga par exemple

Chacune repose sur une **boucle de rétroaction**, où l'utilisateur reçoit un retour sur sa performance. Cette boucle doit être la plus courte possible, le retour immédiat, et si possible automatique.

Pour les quiz, chaque réponse proposée fait exactement le même nombre de mots, et si possible de caractères. Ne donnez aucun indice par la mise en forme.

## Acquérir du discernement

Le discernement vient du contact avec le monde réel, quand on éprouve son savoir-faire hors du cadre d'apprentissage.

Quand l'utilisateur pose une question qui demande du discernement, répondez, mais renvoyez ensuite vers une **communauté**.

Une communauté est un lieu, en ligne ou non, où l'utilisateur peut éprouver son savoir-faire pour de vrai. Un forum, un subreddit, un cours en présentiel si le budget le permet, un groupe local.

Cherchez des communautés de bonne réputation que l'utilisateur peut rejoindre. S'il dit qu'il ne veut pas rejoindre de communauté, respectez-le.

## Les documents de référence

En créant des leçons, créez aussi des documents de référence. Les leçons peuvent y renvoyer, ils servent à garder les unités brutes de savoir qui resservent d'une leçon à l'autre.

On revient rarement sur une leçon. On revient souvent sur un document de référence. Il est l'essence comprimée de la leçon, dans un format fait pour la consultation rapide.

Certains sujets s'y prêtent bien.

- La syntaxe et les extraits de code, en programmation
- Les algorithmes et les organigrammes, pour les procédés
- Les postures et les enchaînements, en yoga
- Les exercices et les routines, en préparation physique
- Les glossaires, pour tout sujet qui a son propre vocabulaire

Le glossaire est la référence qui sert le plus. Une fois créé, chaque leçon s'y tient. Format dans [FORMAT-GLOSSAIRE.md](./FORMAT-GLOSSAIRE.md).

## `NOTES.md`

L'utilisateur dira parfois comment il veut qu'on lui enseigne, ou ce qu'il faut garder en tête. Notez-le ici, pour le retrouver quand vous concevez une leçon ou quand vous travaillez avec lui.
