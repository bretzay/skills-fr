# skills-fr

Des compétences d'agent en français. Claude Code, Codex, Cursor, Gemini, Copilot, Windsurf, opencode et une quinzaine d'autres.

Les meilleures *skills* publiées aujourd'hui sont écrites en anglais, et un agent suit toujours mieux une consigne dans la langue où on lui parle. Ce dépôt traduit celles qui valent le détour, avec le vocabulaire français du domaine plutôt qu'un calque, et garde la trace exacte de leur origine.

Rien ici n'est attaché à un éditeur. Une compétence est un dossier avec un `SKILL.md` dedans, au format [Agent Skills](https://code.claude.com/docs/en/skills), un standard ouvert que lisent aujourd'hui une vingtaine d'agents.

| Compétence | Ce qu'elle fait |
|---|---|
| **apprendre** | Transforme un dossier vide en espace d'apprentissage suivi, session après session |

Traduit de [`teach`](https://github.com/mattpocock/skills/tree/main/skills/productivity/teach), par [Matt Pocock](https://github.com/mattpocock), sous licence MIT. Voir [NOTICE.md](./NOTICE.md) pour la provenance exacte et les choix de traduction.

## apprendre

Vous ouvrez un dossier vide, vous demandez à apprendre la fermentation du pain au levain, et l'agent commence par vous demander pourquoi. Pas pour faire joli. Sans raison concrète, il n'a aucun moyen de choisir quoi vous enseigner en premier.

L'appel dépend de votre agent.

| Agent | Invocation |
|---|---|
| Claude Code | `/apprendre la fermentation du levain` |
| Codex | `$apprendre la fermentation du levain` |
| Les autres | « utilise la compétence apprendre, je veux apprendre la fermentation du levain » |

Ensuite l'agent construit un cours autour de vous, dans ce dossier.

```
mon-apprentissage/
├── MISSION.md                  pourquoi vous apprenez ça, la boussole de tout le reste
├── RESSOURCES.md               les sources de confiance, triées et annotées
├── GLOSSAIRE.md                le vocabulaire du sujet, une fois que vous le maîtrisez
├── NOTES.md                    vos préférences, comment vous voulez qu'on vous enseigne
├── lecons/
│   └── 0001-autolyse.html      une leçon courte, belle, interactive, à imprimer
├── fiches-apprentissage/
│   └── 0001-hydratation.md     ce que vous avez compris, et ce que ça change pour la suite
├── reference/
│   └── ratios.html             l'aide-mémoire qu'on rouvre, contrairement aux leçons
└── composants/
    └── style.css               réutilisé par toutes les leçons, pour que ça fasse un cours
```

Ce qui distingue cette compétence d'un simple « explique-moi X » tient en trois idées.

**L'état persiste.** Les fiches d'apprentissage disent ce que vous savez déjà. La session suivante les lit et reprend au bon endroit, sans réexpliquer ce qui est acquis ni sauter ce qui manque.

**La difficulté est dosée.** L'agent vise la zone proximale de développement, le point où vous êtes sollicité juste ce qu'il faut. Pour le savoir, la difficulté est l'ennemi, elle mange la mémoire de travail. Pour le savoir-faire, elle devient l'outil, c'est l'effort de rappel qui fait tenir les choses.

**Les sources priment sur le modèle.** L'agent a pour consigne de ne jamais faire confiance à ses connaissances paramétriques. Il cherche des sources, les range dans `RESSOURCES.md`, et crible les leçons de citations.

## Installation

### Tous agents, une commande

```bash
npx skills@latest add bretzay/skills-fr
```

L'installeur détecte les agents présents sur votre machine et vous demande lesquels servir. Il connaît Claude Code, Codex, Cursor, GitHub Copilot, Windsurf, Gemini, Cline, Amp, opencode, Zed, Roo, Kilo, Goose, Droid, Trae, Antigravity et quelques autres.

Quelques options qui servent.

```bash
npx skills@latest add bretzay/skills-fr --list         # voir le contenu sans rien installer
npx skills@latest add bretzay/skills-fr --agent '*'    # tous les agents détectés
npx skills@latest add bretzay/skills-fr --global       # au niveau utilisateur, pas dans le projet
npx skills@latest add bretzay/skills-fr --copy         # copier au lieu de lier, pour modifier
npx skills@latest update apprendre                     # récupérer les corrections
```

### À la main

Une compétence est un dossier. Copiez-le là où votre agent va le chercher.

| Agent | Dans un projet | Pour tous vos projets |
|---|---|---|
| Claude Code | `.claude/skills/` | `~/.claude/skills/` |
| Codex | `.agents/skills/` | `~/.agents/skills/` |

```bash
git clone https://github.com/bretzay/skills-fr
cp -r skills-fr/skills/apprendre ~/.claude/skills/apprendre    # Claude Code
cp -r skills-fr/skills/apprendre ~/.agents/skills/apprendre    # Codex
```

Si votre agent n'est pas dans le tableau, cherchez « skills » dans sa documentation. Le dossier attendu est presque toujours `<config-de-l-agent>/skills/`, et le contenu à y déposer est le même.

C'est la route à prendre si vous voulez modifier les fichiers. Ce ne sont que des Markdown, ils vous appartiennent, adaptez-les.

### Claude Code, en plugin

Confort supplémentaire pour les utilisateurs de Claude Code, qui ajoute les mises à jour automatiques. Ce n'est pas la route principale, juste la plus courte sur cet agent-là.

```
/plugin marketplace add bretzay/skills-fr
/plugin install skills-fr@bretzay
```

Dans tous les cas, une compétence fraîchement installée devient active à la **session suivante**. Les agents lisent leurs compétences au démarrage, pas en cours de route.

## Ce que chaque agent lit

Le frontmatter de `SKILL.md` se lit à deux vitesses.

| Champ | Qui le lit |
|---|---|
| `name` | tous, c'est le standard |
| `description` | tous, c'est le standard |
| `disable-model-invocation` | Claude Code seul, ignoré ailleurs |
| `argument-hint` | Claude Code seul, ignoré ailleurs |
| `agents/openai.yaml` | Codex seul, ignoré ailleurs |
| `upstream_*` | personne, c'est de la provenance pour les humains |

Un agent qui ne connaît pas un champ l'ignore, le standard le prévoit. Le corps de la compétence est du Markdown ordinaire, qu'aucun agent n'interprète de travers.

Les deux champs de contrôle disent la même chose dans deux dialectes. N'invoque pas cette compétence de toi-même, attends que l'utilisateur la demande. Les agents qui n'ont ni l'un ni l'autre s'appuient sur la description, qui le dit en clair.

## Une première session

```bash
mkdir ~/apprendre-le-droit-des-contrats && cd $_
```

Lancez votre agent dans ce dossier, puis demandez-lui d'apprendre le droit des contrats avec la compétence `apprendre`.

Il vous interroge d'abord. Répondez concrètement. « Comprendre le droit des contrats » ne lui sert à rien, « relire moi-même mes contrats de prestation au lieu de payer un avocat à chaque fois » lui dit tout. Il écrit `MISSION.md`, cherche des sources, remplit `RESSOURCES.md`, puis produit la première leçon et l'ouvre dans votre navigateur.

À la fin de la leçon, posez-lui vos questions. Il est votre professeur, pas un distributeur de pages.

Revenez le lendemain, dans le même dossier, et redemandez-lui la compétence. Il relit vos fiches, voit où vous en êtes, et enchaîne.

## Traduire une autre compétence

Les *pull requests* sont bienvenues. Quatre règles, tirées de ce qui a servi ici.

1. **Le vocabulaire du domaine, pas le mot-à-mot.** *Zone of proximal development* est « zone proximale de développement » parce que c'est le terme que Vygotski a en français, pas parce que les mots correspondent.
2. **Le standard d'abord.** `name` et `description` portent le sens. Tout champ propre à un agent va après, et ne doit jamais être nécessaire pour que la compétence fonctionne ailleurs.
3. **La provenance dans le frontmatter.** `upstream_repo`, `upstream_path`, `upstream_commit`, `upstream_release`. Sans le commit, personne ne saura jamais ce qui a changé en amont.
4. **Les écarts documentés dans `NOTICE.md`.** Un ajout, une suppression, un exemple remplacé, ça se dit. C'est ce qui sépare une traduction d'une réécriture silencieuse.

Vérifiez avant d'ouvrir la PR.

```bash
npx skills@latest add <votre-fork> --list    # la compétence est vue et décrite correctement
claude plugin validate .                     # les manifestes du plugin, si vous y touchez
```

## Licence

MIT, comme le dépôt d'origine. L'oeuvre anglaise est de Matt Pocock, la traduction d'Aurélien Damoizeau ([Dalgis Kest](https://github.com/bretzay)). Les deux mentions figurent dans [LICENSE](./LICENSE).
