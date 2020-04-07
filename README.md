# git-example

## Dependances

- `git`
  - Linux : Pour la plupart des distribution, `git` est inclut.
  - macOS : Il faut d'abord installer les programmes de lignes de commandes
    ```bash
    xcode-select --install
    ```
  - Windows, telecharger [Git for Windows](https://gitforwindows.org)

- `bash`
  - Inclut dans les distribution Linux & macOS
  - Inclut dans Git Bash (Git for Windows)
  - Antiseche : https://github.com/LeCoupa/awesome-cheatsheets/blob/master/languages/bash.sh

## Premiers pas

### Configurer `git`
D'abord, si on n'a jamais utilisé git, il faut configurer son "user" git. Ceci va juste servir a indentifier qui a fait des modifications (en l'occurence vous).

```bash
git config --global user.name "Jean Bonneau"
git config --global user.email "jean.bonneau@charcuterie.com"
```

Si vous voulez configurer cet identifier pour le projet en cours seulement, lachez l'option `--global`. Cela peut arriver si vous travaillez pour une organisation/société sur un projet en particulier.

```bash
git config user.name "Jean Bonneau"
git config user.email "jean.bonneau.pro@charcuterie-pro.com"
```

Pour que `git` se souvienne de votre mot de passe, il faut le configurer en conséquence.

1. Windows
```bash
git config --global credential.helper wincred
```
2. Linux
```bash
git config --global credential.helper cache
```
3. macOS
```bash
git config --global credential.helper osxkeychain
```

### Cloner le projet
Avant toutes choses, il faut "cloner" le projet. Pour ce projet, il faut faire.

D'abord, aller 
```bash
git clone https://github.com/Clovel/git-example.git
```

### Faire des modifications
Faites des modification a un fichier avec l'editeur de texte/code de votre choix.

### Afficher les modifications
Maintenant que vous avez modifié votre fichier (par ex. `README.md`), vous verez les modifications avec la commande suivante :
```bash
git status
```
ou sa variante courte
```bash
git status --short
```
Par exemple, si je modifie le fichier `README.md` sur la branche `mabranche`, le resultat sera :
```
On branch mabranche
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```
ou, en version courte :
```
 M README.md
```

Si votre terminal st compatible avec les couleurs, le nom du fichier sera surligné en rouge.

### Preparer les fichiers à etre versionnés
Avant de `commit` nos modifications, il faut "ajouter" nos modifications.

Par exemple, si j'ai modifié le fichier `README.md`, je fais :
```bash
git add README.md
```

En faisant `git status`, vous verez :
```
On branch mabranche
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   README.md

```

Si votre terminal st compatible avec les couleurs, le nom du fichier sera surligné en rouge.

Si j'ai plusieurs modifications à ajouter à la fois, je fais :
```bash
git add Class.hpp Class.cpp main.cpp
```

### Faire un commit
Un commit est (en gros) un groupement de modifications. Il ne contient pas les nouvelles versions des fichiers, mais uniquement la différence entre lui-même et le commit précédent.

La somme de tous les commit donne l'état actuel de votre projet.

Maintenant que j'ai ajouté toutes les modifications que je souhaite ajouter a ma branche, je `commit` celles-ci : 
```bash
git commit
```

Cella va ouvrir un editeur de texte. Par défault, c'est souvent `vi` qui est assez compliquer a prendre en main (mais super efficace quand on le maitrise !). Vous pouvez configurer l'éditeur par defaut avec un commande de configuration : 
```bash
git config (--global) core.editor emacs
```

Voici une liste (non-exhaustive) d'exemples : 

| Editeur                   | Commande de configuration                       |
| ------------------------- | ----------------------------------------------- |
| Atom                      | `git config --global core.editor "atom --wait"` |
| nano                      | `git config --global core.editor nano`          |
| vi                        | `git config --global core.editor vi`            |
| VIM                       | `git config --global core.editor vim`           |
| emacs                     | `git config --global core.editor emacs`         |
| Sublime Text (Mac)        | `git config --global core.editor "subl -n -w"`  |
| Sublime Text (Win 32-bit) | `git config --global core.editor "'c:/program files (x86)/sublime text 3/sublimetext.exe' -w"` |
| Sublime Text (Win 64-bit) | `git config --global core.editor "'c:/program files/sublime text 3/sublimetext.exe' -w"` |

Mais le plus simple, c'est encore de ne pas utiliser un editeur de texte pour ses commits, mais plutot de donner son titre de commit comme ceci :
```bash
git commit -m "Mon commit fait ceci et cela"
```

Si je veux rajouter des details a mon commit, je fait ceci : 
```bash
git commit -m "Mon commit fait ceci et cela" -m "Parce que il fallait corriger ce truc"
```

Si on a configuré son adresse email avec `git config`, on peut rejouter sa signature simple au commit. C'est très utilisé dans le monde de l'Open Source, et certains chefs de projet l'imposent.
```bash
git commit -s -m "Mon commit fait ceci et cela"
```

### Pousser son code
Une fois que nous avons fait nos commits (un ou plusieurs, on peut attendre), il faut pousser sur code sur le dépot distant (s'il y en a un).
```bash
git push <nom_du_depot_distant> <nom_de_la_branche>
```

Le plus souvent, on se contente de
```bash
git push
```

#### Forcer `git push`
En cas de probleme, on peut forcer le `git push` :
```bash
git push --force
```

Attention, c'est très dangereux. Vous risquez d'écraser le code qui est sur le distant. Cette commande ne doit être lancée que par quelqu'un qui sait ce qu'il fait et qui a le pouvoir décisionnel sur le projet. 

En général, si un developpeur a besion de cette commande, c'est qu'il est :
- Pas a jour avec le dépot distant
- Pas sur la bonne branche

### Récuperer du code. 
Pour récuperer le code distant, il faut utiliser la commande `git pull`
Si on se place sur la branche `mabranche`, et que l'on veux récuperer le contenu de la branche `mabranche` qui est sur le dépot distant, on fait : 
```bash
git pull
```

Cette commande est en realité la combinaison de deux autres commandes, et équivaut à :
```bash
git fetch
git merge FETCH_HEAD
```

Si on est en retard avec le dépot distant mais que l'on a fait des commits en local, `git` va essayer de s'arranger pour ne pas causer de conflit en faisant un merge :

```
          A---B---C origin/mabranche
         /         \
    D---E---F---G---H mabranche
```

Si vous voulez eviter cela, faites un `git fetch` avant et vérifiez si vous etes en retard. Pour garder un historique de commits propre, il faut eviter ce genre de situation.

## Les branches
Pour eviter que tout le monde se marche sur les pieds, on utilise des branches. De cette facon, on aura pas de problèmes au moment de `push`/`pull`.
           A---B---C  Clovel
          /       I---J---K  Cahmcam
         /       /
    D---E---F---G---H  master
                     \
                      L---M  logg06

Cela permet egalement de developper indépendamment différentes fonctionnalités.

```
           A---B---C  serveur
          /       I---J---K  client
         /       /
    D---E---F---G---H  master
                     \
                      L---M  bouton
```

Pour savoir sur quelle branche on se trouve on peut faire :
```bash
git branch --show-current
```

Pour changer de branche courante, on fait :
```bash
git checkout une-branche
```

Pour créer une nouvelle branche puis y aller, on fait :
```bash
git checkout -b ma-nouvelle-branche
```

Pour revenir a la branche précédente, on peut faire :
```
git checkout -     # Pas l'underscore, le "tiret du 6"
```

#### Attention
Les branches ne doivent pas contenir d'espaces

## Le "Merge"
Faire un merge, c'est fusionner le code d'une branche dans une autre.

Cela permet de se mettre à jour avec une branche de référence qui évolue par exemple.
```
          A---B---m1--M---m2--M  mabranche
         /       /       /
    D---E---F---G---H---I---J---K---L branche-de ref
```

On se sert aussi des merge pour "publier" son code.
```
          A---B---C  mabranche
         /         \
    D---E---F---G---m1  master
```

Pour réaliser un merge, on se place sur la branche de destintion, puis on "merge" la branche d'origine :
```
          A---B---C  mabranche (je suis ici)
         /
    D---E---F---G  master
```
On fait :
```bash
git checkout master
git merge mabranche
```
On se retrouve avec
```
          A---B---C  mabranche
         /         \
    D---E---F---G---m1  master (je suis ici)
```

## Le "Rebase"
Le rebase est l'alternative du merge. Il permet de placer nos commit par-dessus ceux de l'autre branche.
Par exemple, si on est dans la configuration suivante :
```
          A---B---C  mabranche (je suis ici)
         /
    D---E---F---G  master
```

Et que l'on souhaite se mettre a jour avec la branche `master`, on peut faire :
```bash
git rebase master
```
Et on se retrouve avec :
```
                  A'--B'--C'  mabranche (je suis ici)
                 /
    D---E---F---G  master
```

Cela fonctionne en cherchant l’ancêtre commun le plus récent des deux branches (celle sur laquelle vous vous trouvez et celle sur laquelle vous rebasez), en récupérant toutes les différences introduites par chaque `commit` de la branche courante, en les sauvant dans des fichiers temporaires, en réinitialisant la branche courante sur le même commit que la branche de destination et en appliquant finalement chaque modification dans le même ordre.

## Corriger le commit précédent
Il se peut que l'on a fait un erreur dans le commit précédent. Pour cela, il y a la commande `git commit --amend`.

1. Si on veut corriger le nom du commit précédent :
Dans ce cas, on peut faire :
```bash
git commit --amend
```
ce qui ouvira l'éditeur par défaut pour pouvoir editer le nom/la description du commit.

2. Si on veut rajouter des modifications dans le commit précédent :
```bash
git add UnFichierModifie.js UnDeuxiemeFichierModifie.js
git commit --amend
```

On peut aussi faire cette operation sans vouloir changer le nom du commit :
```bash
git add UnFichierModifie.js UnDeuxiemeFichierModifie.js
git commit --amend --no-edit
```

## Le rebase interactif
TODO

# Des interaces graphiques (GUI) pour `git`
Utiliser la ligne de commande pour git est le plus facile et le plus pratique pour faire des operations. Néanmoins, il est parfois utile d'avoir des outils supplémentaires pour accélerer le process `git` ou pour mieux visualiser ce qu'il se passe. Voici quelques exemples :
- [tig](https://github.com/jonas/tig) : Permet de visualiser les branches dans le ligne de commande. - Win, Linux, macOS - Open Source (GPL-2.0)
- [GitKraken](https://www.gitkraken.com) - Win, Linux, macOS - Axosoft
- [Tower](https://www.git-tower.com/) - Win, macOS - fournova
- [SourceTree](https://www.sourcetreeapp.com) - Win, macOS - Atlassian
- [GitAhead](https://github.com/gitahead/gitahead) - Win, Linux, macOS - Open Source (MIT)
