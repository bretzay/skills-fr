# Format de `MISSION.md`

`MISSION.md` est à la racine de l'espace de travail. Il dit _pourquoi_ l'utilisateur apprend ce sujet. Chaque décision d'enseignement, quoi enseigner ensuite, quelles ressources sortir, quels exercices concevoir, remonte à ce document.

## Modèle

```md
# Mission : {Sujet}

## Pourquoi
{1 à 3 phrases. L'objectif concret et réel que l'utilisateur poursuit. Qu'est-ce qui change dans sa vie ou dans son travail quand il a ce savoir-faire ? Évitez les formulations abstraites du genre « comprendre X », creusez jusqu'au résultat attendu.}

## À quoi on verra que c'est gagné
- {Une chose précise et observable que l'utilisateur saura faire}
- {Une autre}
- {…}

## Contraintes
- {Temps, budget, engagements déjà pris, préférences d'apprentissage, tout ce qui borne l'approche}

## Hors sujet
- {Les sujets voisins que l'utilisateur ne veut pas poursuivre maintenant, ce qui protège la zone proximale de développement}
```

## Règles

- **Une mission par espace de travail.** Si l'utilisateur veut apprendre deux choses sans rapport, cela fait deux espaces.
- **Du concret plutôt que de l'abstrait.** « Courir un semi-marathon en octobre » vaut mieux que « me remettre en forme ». « Livrer un outil en ligne de commande en Rust à mon équipe » vaut mieux que « apprendre Rust ».
- **Poussez contre le flou.** Si l'utilisateur n'arrive pas à dire pourquoi, interrogez-le avant d'écrire quoi que ce soit. Une mauvaise mission est pire que pas de mission du tout.
- **Révisez quand la réalité bouge.** Les missions changent. Quand l'objectif de l'utilisateur se déplace, mettez ce fichier à jour, ne laissez pas une mission périmée diriger les sessions suivantes.
- **Restez court.** Si `MISSION.md` dépasse un écran, ce n'est plus une boussole, c'est un plan.
