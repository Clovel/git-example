# git-example

## Dependances

- `git`
  - Linux : Pour la plupart des distribution, `git` est inclut.
  - macOS : Il faut d'abord installer les programmes de lignes de commandes
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

## Faire des modifications
Faites des modification a un fichier avec l'editeur de texte/code de votre choix.

## Commit des modifications
Maintenant que vous avez modifié votre fichier (par ex. `README.md`), vous verez les modifications avec la commande suivante :
```bash
git status
```
ou sa variante courte
```bash
git status --short
```

MON BOOOOOO SAPIIIIIIN


Toto fait du ski dans les bois

