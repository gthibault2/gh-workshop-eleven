# Workshop - Make Github great again ... mais sans navigateur

> L'objectif de ce projet est d'apprendre à utiliser le CLI de Github d'une manière plus ludique que la lecture de la documentation.  
> Pour ce faire, nous avons besoin d'un MJ (maitre du jeu), de créer une organisation Github temporaire et de forker ce repo.  
> Enfin, il doit configure le nouveau repo ainsi:
> - créer un secret `MAGIC_NUMBER` avec un nombre aléatoire qui sera utilisé comme [sel](https://fr.wikipedia.org/wiki/Salage_(cryptography)) (`Settings > Secret > Actions`)
> - configurer la protection de branche pour interdire tout merge si la CI ne passe pas (`Settings > Branches > Add rule` puis cocher `Require a pull request before merging`, `Require review from Code Owners`, `Require status checks to pass before merging` et mettre `Play round` dans `Status checks that are required.`)

## Objectif

L'objectif est simple, trouver le bon numéro pour être le premier à valider sa PR.

## Déroulement

1. Chaque utilisateur doit créer un problème avec le titre `[New Player] LOGIN_GITHUB` et le commenter avec `/invite-me` pour être accepté dans le jeu.  
    À ce stade, le *MJ* doit inviter l'utilisateur dans l'organisation et fermer le ticket.
2. Le nouvel arrivant doit ajouter un fichier `player_LOGIN_GITHUB` avec un numéro dedans et créer une `Pull Request`. Tant que cette *PR* n'est pas valide *(aka. tant que le numéro n'est pas trouvé)*, il devrait la modifier.  
    Les indices pour trouver ce numéro seront disponibles dans les artefacts CI (`indice_LOGIN_GITHUB`).
3. Le premier à valider sa *PR* gagne.

## Règles
1. ~~Il est interdit de parler du F~~ ... pardon, mauvais livret
1. Il est interdit d'utiliser le navigateur
2. Il est interdit d'utiliser le navigateur
3. Il est encore interdit d'utiliser le navigateur

## **DW**RTFM *(**Don't Want** Read The F*****g Manual)*

Voici quelques commandes qui vous seront utiles tout au long du jeu:

- Cloner un repo: `git clone <URL>`
    > **NOTE:** on pourrait utiliser `gh repo clone <ORG/REPO>`, mais comme le repo actuel est un fork, la création de PR va être plus compliqué du fait qu'il va y avoir deux repos distant (l'original et le fork).  
    > Dans un context de tout les jours, `gh repo clone` est largement suffisamment.
- Faire un fork: `gh repo fork`  
    > **NOTE:** il faut savoir que l'on est pas obligé de faire un fork immédiatement; cela nous sera demandé lors de la création d'une PR
- Créer une issue: `gh issue create`
- Commenter une issue: `gh issue comment`
- Lister les issues: `gh issue list [FILTRE]` ou `gh issue status`  
    > **NOTE:** j'aime bien personnellement la deuxième parce qu'elle énumère tous les résultats, mais en différenciant ceux qui nous sont assignés.
- Ouvrir une issue: `gh issue view ISSUE_ID`  
    > **NOTE:** il faut savoir que le CLI utilise très souvent la branche actuelle pour faire un filtrage. Par exemple `gh pr view` n'affichera que la PR correspondante à la branche courante, si elle existe
- Créer une *PR*: `gh pr create` 
    > **NOTE:** j'ai pour habitude de toujours ajouter `--draft` à mes PRs. Cela évite de notifier les personnes tant que la PR n'est pas prête à être review. Il me suffit ensuite de faire `gh pr ready`.  
    > Une grande partie des commandes utilisables avec les issues le sont également pour les PRs, donc je ne vais pas m'attarder dessus.
- Merger une PR: `gh pr merge`
- Lister les workflows lancés via *Github Action*: `gh run list`
- Suivre un workflow en temps réel: `gh run watch`
- Avoir des info sur un workflow précis: `gh run view`
- Télécharger un artéfact *(une archive uploadé par la CI)*: `gh run download`  
    > **NOTE:** avec cette commande, on voit tous les artéfacts.

- Pour avoir une documentation assez exhaustive sur le CLI: `gh reference`
    > **NOTE:** cette NOTE ne sert absolument à rien

### Petits rappel GIT pour les non initiés

- Créer une nouvelle branche: `git switch --create LOGIN_GITHUB`
- Ajouter le fichier `player_LOGIN_GITHUB` à l'index actuel *(instantané du contenu du repo)*: `git add player_LOGIN_GITHUB`
- Enregistrer les modifications: `git commit -m "$(curl -s http://whatthecommit.com/index.txt)"` **(A NE PAS FAIRE POUR LES REPOS DU BOULOT,** sauf le vendredi soir **)**
- Envoyer les modifications sur le repository distant: `git push`

## Pourquoi faire un workshop avec ce format

En rédigeant l'atelier, je me suis rendu compte que faire des minutes d'explication avec quelques exemples était ennuyeux (pour moi mais aussi pour le public).  
J'ai donc essayé d'utiliser un format plus dynamique, accessible à tous et pas seulement à un public de développeurs.

Ce jeu vous permet de pratiquer ce que vous faites habituellement sur un repo normal ;
- Créer, lister et commenter des issues
- Créer, mettre à jour et merger des PRs
- Voir ou attendre le passage du CI et récupérer des artefacts (par exemple, les résultats du TU ou autres).

## PETIT BONUS *(c'est pour cela qu'il est écrit en p'tit)*

Un gros point intéressant du CLI Github, est qu'il est assez facilement extensible (https://github.com/topics/gh-extension).

Voici une petit liste personnelle d'extension que j'utilise tout les jours:
- https://github.com/seachicken/gh-poi: supprime automatiquement les branches locales qui n'existent plus sur le repo distant (PRs mergées uniquement)
- https://github.com/matt-bartel/gh-clone-org: permet de cloner tout les repos d'une organisation
- https://github.com/mislav/gh-branch: liste les branches locales et donne le numéro de PR si il y en a qui sont reliées à des PRs
- https://github.com/dlvhdr/gh-dash: dashboard pour lister les issues/PRs en fonction de certains critères (par exemple en review ou les dependabots)
