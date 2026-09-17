# skills-fr

Des compétences d'agent en français, pour Claude Code.

Les meilleures *skills* publiées aujourd'hui sont écrites en anglais, et un agent suit toujours mieux une consigne dans la langue où on lui parle. Ce dépôt traduit celles qui valent le détour, avec le vocabulaire français du domaine plutôt qu'un calque, et garde la trace exacte de leur origine.

| Compétence | Commande | Ce qu'elle fait |
|---|---|---|
| **apprendre** | `/apprendre <sujet>` | Transforme un dossier vide en espace d'apprentissage suivi, session après session |

Traduit de [`teach`](https://github.com/mattpocock/skills/tree/main/skills/productivity/teach), par [Matt Pocock](https://github.com/mattpocock), sous licence MIT. Voir [NOTICE.md](./NOTICE.md) pour la provenance exacte et les choix de traduction.

## `/apprendre`

Vous ouvrez un dossier vide, vous tapez `/apprendre la fermentation du pain au levain`, et l'agent commence par vous demander pourquoi. Pas pour faire joli. Sans raison concrète, il n'a aucun moyen de choisir quoi vous enseigner en premier.

Ensuite il construit un cours autour de vous, dans ce dossier.

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

### Claude Code

Dans une session, deux commandes.

```
/plugin marketplace add bretzay/skills-fr
/plugin install skills-fr@bretzay
```

Ou depuis le terminal.

```bash
claude plugin marketplace add bretzay/skills-fr
claude plugin install skills-fr@bretzay
```

Une compétence fraîchement installée devient active à la **session suivante**. Claude lit les compétences au démarrage, pas en cours de route.

### Cowork

Personnaliser, puis Plugins, puis Ajouter une marketplace, puis `bretzay/skills-fr`.

### À la main

Copiez le dossier où votre agent va le chercher.

```bash
git clone https://github.com/bretzay/skills-fr
cp -r skills-fr/skills/apprendre ~/.claude/skills/apprendre     # partout
cp -r skills-fr/skills/apprendre .claude/skills/apprendre       # ce projet seulement
```

C'est la route à prendre si vous voulez modifier les fichiers. Ce ne sont que des Markdown, ils vous appartiennent, adaptez-les.

## Une première session

```bash
mkdir ~/apprendre-le-droit-des-contrats && cd $_
claude
```

```
> /apprendre le droit des contrats
```

L'agent vous interroge d'abord. Répondez concrètement. « Comprendre le droit des contrats » ne lui sert à rien, « relire moi-même mes contrats de prestation au lieu de payer un avocat à chaque fois » lui dit tout. Il écrit `MISSION.md`, cherche des sources, remplit `RESSOURCES.md`, puis produit la première leçon et l'ouvre dans votre navigateur.

À la fin de la leçon, posez-lui vos questions. Il est votre professeur, pas un distributeur de pages.

Revenez le lendemain, dans le même dossier.

```
> /apprendre
```

Il relit vos fiches, voit où vous en êtes, et enchaîne.

## Traduire une autre compétence

Les *pull requests* sont bienvenues. Trois règles, tirées de ce qui a servi ici.

1. **Le vocabulaire du domaine, pas le mot-à-mot.** *Zone of proximal development* est « zone proximale de développement » parce que c'est le terme que Vygotski a en français, pas parce que les mots correspondent.
2. **La provenance dans le frontmatter.** `upstream_repo`, `upstream_path`, `upstream_commit`, `upstream_release`. Sans le commit, personne ne saura jamais ce qui a changé en amont.
3. **Les écarts documentés dans `NOTICE.md`.** Un ajout, une suppression, un exemple remplacé, ça se dit. C'est ce qui sépare une traduction d'une réécriture silencieuse.

Vérifiez avant d'ouvrir la PR.

```bash
claude plugin validate .
```

## Licence

MIT, comme le dépôt d'origine. L'oeuvre anglaise est de Matt Pocock, la traduction d'Aurélien Damoizeau ([Dalgis Kest](https://github.com/bretzay)). Les deux mentions figurent dans [LICENSE](./LICENSE).
