# Git & GitHub

## Introduction

Git...

* permet de gérer du code source (mais pas que), et particulièrement son évolution (versions)
* permet de partager du code source avec des amis, collègues, etc. (collaboration)
* s'utilise principalement en ligne de commande ou dans un IDE

GitHub...

* outil par dessus Git qui fluidifie la collaboration, notamment dans l'Open-Source (mais pas que)
* racheté par Microsoft après avoir été autonome avant
* fournit "GitHub Desktop"... sauf sous Linux :-/

## Git

On parle de "Dépôt" Git. Un dépôt Git est principalement composé:

* d'une base de données qui contient toutes les informations sur l'histoire de votre code
* d'une "copie locale" qui permet d'éditer le contenu à un instant donné
* d'un peu de configuration

### Création d'un dépôt

On veut d'abord initialiser un dépôt Git.

```shell
mkdir git-demo
cd git-demo
git init
```

La base de données est dans `.git` et ses sous-répertoires.

La copie locale c'est tout sauf `.git`, au début il n'y a rien.

`.git` contient aussi la configuration.

### Commit

Ensuite on veut ajouter du contenu dans notre dépôt et l'enregistrer comme un état connu dans l'histoire du dépôt.

* un "commit" est la représentation de cet état
* il contient toutes les différences entre l'état précédent et l'état qui est enregistré
* il possède un identifiant pour le retrouver, il est unique

Pour créer un commit, il faut d'abord créer le contenu dans la "copie locale": `README.md`

```markdown
# Documentation

## Introduction

Cette documentation est divisée en différents chapitres qui ne sont pas encore écrits.

```

Ensuite il faut dire à Git ce que l'on souhaite mettre dans le commit


```shell
git add README.md
```

Ceci a pour conséquence de mettre son contenu actuel dans l'"index" (ou le "cache"). L'index est un espace transitoire dans lequel se trouve tout ce qui doit aller dans le commit et uniquement cela.

Enfin il faut créer le commit:

```shell
git commit
```

On peut maintenant visualiser ce commit avec un outil graphique.

![Premier commit](images/premier-commit.png)

On voit:

* un commit avec son message
* le nom de la branche courante (`main`)
* l'auteur
* la date de création
* l'identifiant du commit
* le contenu

### Ajouts

Pour ajouter du contenu, il suffit de répéter les opérations:

* édition dans la copie locale
* mise dans l'index
* commit

![Chapitre 1](images/chapitre-1.png)

### Branche

Lorsque l'on veut effectuer plusieurs modifications pour les partager plus tard, il suffit de créer une branche:

```shell
git checkout -b branche-1
```

![Branche 1](images/branche-1.png)

* la branche 1 contient 2 ajouts
* la branche principale n'a pas bougée

### Fusion (Merge)

Lorsqu'on est content du résultat, on "fusionne" la branche dans la principale:

```shell
git checkout main
git merge --no-ff branche-1
```

![Fusion branche 1](images/merge-branche-1.png)

* la branche 1 n'a pas bougé
* la branche principale a reçu les modifications apportées par la branche 1
* sans `--no-ff`, il n'y aurait pas eu de "commit de fusion" et seule une ligne droite apparaîtrait dans le graphe (et ça serait beaucoup moins drôle)
* le commit de fusion a 2 parents
