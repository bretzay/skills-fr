# Format des fiches d'apprentissage

Les fiches d'apprentissage vivent dans `./fiches-apprentissage/` et se numérotent en séquence, `0001-slug.md`, `0002-slug.md`, et ainsi de suite. Créez le dossier au dernier moment, seulement quand la première fiche s'écrit.

Elles sont l'équivalent pédagogique des décisions d'architecture. Elles gardent les leçons non évidentes, les prises de conscience et le savoir préalable déclaré, tout ce qui dirigera les sessions suivantes. Elles servent à calculer la zone proximale de développement.

## Modèle

```md
# {Titre court de ce qui a été appris ou établi}

{1 à 3 phrases. Ce qui a été appris, ou quel savoir préalable a été établi, et pourquoi cela compte pour les sessions suivantes.}
```

C'est tout le format. Une fiche peut tenir en un paragraphe. Ce qui compte, c'est d'enregistrer _que_ ceci est désormais su, et _pourquoi_ cela change ce qu'il faut enseigner ensuite, pas de remplir des rubriques.

## Rubriques facultatives

Ne les mettez que si elles apportent vraiment quelque chose. La plupart des fiches n'en ont pas besoin.

- **Statut** en frontmatter (`actif | remplacée par FA-NNNN`). Utile quand une compréhension ancienne se révèle fausse et se fait remplacer.
- **Preuve**. Comment l'utilisateur a démontré sa compréhension, une question à laquelle il a répondu, un exercice réussi, une expérience passée citée. Utile quand on pourra revenir sur l'affirmation.
- **Conséquences**. Ce que cela ouvre ou ferme pour les sessions suivantes. À noter quand ce n'est pas évident.

## Numérotation

Parcourez `./fiches-apprentissage/`, prenez le plus grand numéro, ajoutez un.

## Quand écrire une fiche

Écrivez-en une dès que l'un de ces cas se présente.

1. **L'utilisateur a démontré une vraie compréhension de quelque chose de non trivial.** Pas une simple exposition, une preuve qu'il sait employer le concept correctement. Cela relève le plancher de ce qu'il faut enseigner ensuite.
2. **L'utilisateur a déclaré un savoir préalable.** « Je connais déjà X. » Notez-le pour que les sessions suivantes ne le réenseignent pas. Notez aussi la _profondeur_ annoncée.
3. **Une idée fausse a été corrigée.** L'utilisateur croyait quelque chose de faux et voit maintenant pourquoi. Ces fiches valent cher, elles annoncent les obstacles à venir sur les sujets voisins.
4. **La mission a bougé à la suite d'un apprentissage.** L'utilisateur a découvert qu'il tenait à autre chose que ce qu'il croyait. Faites le lien vers [[MISSION.md]] et mettez-le à jour.

### Ce qui ne compte pas

- Ce qui a seulement été couvert. Couvrir n'est pas apprendre. Attendez la preuve.
- Ce qui tient déjà en une entrée de [[GLOSSAIRE.md]]. Ne dupliquez pas.
- Le journal de bord des sessions. Une fiche d'apprentissage n'est pas un journal, c'est une observation qui pèse sur les décisions.

## Remplacement

Quand une fiche plus récente contredit une plus ancienne, parce que la compréhension s'est approfondie ou corrigée, marquez l'ancienne `Statut : remplacée par FA-NNNN` plutôt que de la supprimer. L'histoire de la compréhension est elle-même un signal utile.
