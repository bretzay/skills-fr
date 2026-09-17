# Provenance et choix de traduction

Ce dépôt contient une oeuvre dérivée. Cette page dit d'où elle vient, ce qui a été traduit mot pour mot, et ce qui a été délibérément changé.

## Source

| | |
|---|---|
| Dépôt d'origine | [mattpocock/skills](https://github.com/mattpocock/skills) |
| Auteur | Matt Pocock |
| Chemin | `skills/productivity/teach` |
| Version | `v1.2.3` |
| Commit traduit | `74ca5fe077456a0b3b2f5310cf9430999fd0b5fd` |
| Licence | MIT |

Chaque `SKILL.md` de ce dépôt porte ces quatre informations dans son frontmatter, sous les clés `upstream_repo`, `upstream_path`, `upstream_commit` et `upstream_release`. Claude Code ignore les clés qu'il ne connaît pas, elles ne servent qu'à retrouver la source.

Pour voir ce qui a bougé en amont depuis la traduction :

```bash
git -C /chemin/vers/mattpocock-skills log --oneline 74ca5fe..main -- skills/productivity/teach
```

## Nom de la compétence

`teach` devient `apprendre`. La compétence est invoquée par l'apprenant, pas par l'enseignant, et `/apprendre les réseaux de neurones` se lit mieux en français que l'impératif `/enseigne`.

## Vocabulaire

Le texte anglais s'appuie sur la littérature de la psychologie de l'apprentissage. Les termes ont été rendus par leur équivalent français reçu, pas par un calque.

| Anglais | Français retenu | Note |
|---|---|---|
| zone of proximal development | zone proximale de développement | terme consacré, Vygotski |
| storage strength | force de stockage | Bjork |
| fluency strength | force de restitution | Bjork parle de *retrieval strength*, « restitution » garde l'idée de l'accès immédiat |
| desirable difficulty | difficulté désirable | Bjork |
| retrieval practice | rappel actif | l'usage français en pédagogie |
| spacing | espacement | |
| interleaving | entrelacement | |
| working memory | mémoire de travail | |
| feedback loop | boucle de rétroaction | |
| knowledge / skills / wisdom | savoir / savoir-faire / discernement | la triade native française. « Sagesse » aurait été un calque, le texte parle du jugement qui vient de la pratique réelle |
| learning record | fiche d'apprentissage | l'original les compare aux ADR, la fiche joue le même rôle |
| assets (composants partagés) | composants | le texte anglais les appelle déjà *components*, le dossier suit |
| cheat sheet | aide-mémoire | |
| primary source | source primaire | |
| parametric knowledge | connaissances paramétriques | ce que le modèle croit savoir sans source |

## Fichiers de l'espace de travail

Les artefacts que la compétence produit sont nommés en français, puisque l'apprenant les lit et les édite.

| Original | Ici |
|---|---|
| `MISSION.md` | `MISSION.md` |
| `RESOURCES.md` | `RESSOURCES.md` |
| `GLOSSARY.md` | `GLOSSAIRE.md` |
| `NOTES.md` | `NOTES.md` |
| `lessons/` | `lecons/` |
| `learning-records/` | `fiches-apprentissage/` |
| `reference/` | `reference/` |
| `assets/` | `composants/` |
| `MISSION-FORMAT.md` | `FORMAT-MISSION.md` |
| `RESOURCES-FORMAT.md` | `FORMAT-RESSOURCES.md` |
| `GLOSSARY-FORMAT.md` | `FORMAT-GLOSSAIRE.md` |
| `LEARNING-RECORD-FORMAT.md` | `FORMAT-FICHE-APPRENTISSAGE.md` |

Les noms de dossiers restent sans accent. `lecons` et non `leçons`, `reference` et non `référence`. Un dossier accentué finit toujours par casser quelque part, un shell, une archive zip, un chemin Windows. Les fichiers Markdown que l'apprenant ouvre, eux, gardent leurs accents.

## Portabilité entre agents

L'original est déjà indépendant de l'éditeur, c'est du Markdown au format [Agent Skills](https://code.claude.com/docs/en/skills). La traduction garde cette propriété et la rend explicite.

`name` et `description` sont les deux seuls champs du standard. Ils portent tout le sens, et la compétence fonctionne sur n'importe quel agent conforme avec eux seuls. Le reste du frontmatter est un supplément que les agents qui ne le connaissent pas ignorent.

| Champ | Lu par | Rôle |
|---|---|---|
| `name`, `description` | tous | le standard |
| `disable-model-invocation` | Claude Code | empêche l'invocation automatique |
| `argument-hint` | Claude Code | le texte grisé après la commande |
| `agents/openai.yaml` | Codex | métadonnées d'interface et `allow_implicit_invocation` |
| `upstream_*` | personne | provenance, pour les humains |

`disable-model-invocation: true` et `allow_implicit_invocation: false` disent la même chose dans deux dialectes. La compétence ne part pas toute seule, l'utilisateur la demande. C'était déjà l'intention de l'original, qui portait les deux.

Les emplacements d'installation diffèrent d'un agent à l'autre, `.claude/skills/` pour Claude Code, `.agents/skills/` pour Codex. Le contenu déposé, lui, est identique. Le [README](./README.md) donne le tableau complet.

## Écarts assumés

Quatre changements de fond, tout le reste est une traduction fidèle.

1. **Le lien vers `FORMAT-GLOSSAIRE.md` a été ajouté.** L'original livre bien `GLOSSARY-FORMAT.md` mais ne le référence nulle part depuis `SKILL.md`, donc l'agent ne le trouve jamais. Le lien est posé dans la section sur les documents de référence.
2. **Une phrase sur les noms de dossiers sans accent a été ajoutée** au début de `SKILL.md`. Elle n'a pas d'équivalent en anglais, où la question ne se pose pas.
3. **Les tirets cadratins ont été supprimés**, ainsi que les deux-points employés comme connecteurs en milieu de phrase. La ponctuation française porte les mêmes liaisons avec une virgule ou un point.
4. **La `description` précise qu'il faut une demande explicite de l'utilisateur.** L'original s'en remet à `disable-model-invocation` et à `allow_implicit_invocation`, que Claude Code et Codex comprennent. Les autres agents n'ont ni l'un ni l'autre, et la description est alors le seul garde-fou. Dire la condition en clair la rend portable.

Les exemples du domaine de la musculation (hypertrophie, surcharge progressive, RPE) et les sources anglaises citées en exemple ont été gardés tels quels. Un exemple sert à montrer une forme, le remplacer par un exemple français n'aurait rien appris de plus.

## Remerciements

Merci à [Matt Pocock](https://github.com/mattpocock) d'avoir publié ses compétences sous licence MIT. Si l'anglais ne vous gêne pas, allez voir [le dépôt d'origine](https://github.com/mattpocock/skills), il en contient une vingtaine d'autres.
