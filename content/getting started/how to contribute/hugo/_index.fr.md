---
title: hugo
weight: 5
pre: "<b>5. </b>"
disableToc: true
---



Bonjour et bienvenue!

Ce manuel vous montrera comment exécuter Hugo et son serveur Hugo directement à partir de votre ligne de commande!

Avec l’aide de Hugo, vous pouvez créer, afficher, améliorer les entrées pour la base de connaissances et contribuer à la communauté PIRL.

## Vue d'ensemble

Ce guide explique comment télécharger, configurer et exécuter Hugo et son serveur Hugo:


{{< imagesurlsheaders "cloud/Hugo.JPG" >}}


## Conditions préalables

Pour garantir le succès de cette opération, vous aurez besoin de ces conditions:

* connexion Internet
* [Téléchargez la dernière version du binaire Hugo (> 0.25) pour votre système d'exploitation](https://github.com/gohugoio/hugo/releases)
*Téléchargez le repo pirl-docs à partir d'ici: [Pirl-docs](https://git.pirl.io/community/pirl-docs)
* Navigateur Web de votre choix et un peu de volonté

## Action!


### 1) Mac iOS
Si vous êtes un utilisateur Mac, installez Hugo avec une commande simple et puissante.

Command:
brew install Hugo

Suivez le guide d'installation [ici](https://gohugo.io/getting-started/quick-start/)

### 2) Windows OS
* Si vous utilisez Windows comme moi, téléchargez simplement la dernière version de [Hugo](https://github.com/gohugoio/hugo/releases) pour Windows si vous ne l'avez pas encore fait.
* Télécharger le plus récent [Dépositaire de fichiers de documentation PIRL](https://git.pirl.io/community/pirl-docs) isi vous ne l'avez pas encore fait. Décompressez / extrayez ces deux dossiers.
* Ensuite, allez dans le dossier Hugo et copiez tout ce que vous y trouverez.
* Accédez au dossier de la documentation PIRL, passez tous les fichiers HUGO et réécrivez-les si nécessaire.
* Ensuite, appuyez sur le bouton de recherche situé à côté du bouton de démarrage principal de Windows dans le coin inférieur gauche (en général, il se trouve ici :))
* Écrivez un CMD dans la ligne vide et appuyez sur Entrée.
* Maintenant, vous pouvez voir exactement ce que je dois écrire chaque fois que je veux exécuter le serveur Hugo et écrire un article de la Base de connaissances (KB).
* Je dois d’abord localiser ma destination (dans ce cas, il s’agit d’un disque D et de quelques dossiers supplémentaires). Ensuite, je vais me diriger vers le dossier Hugo.

Commandes dans CMD:

1. C:\Users\YourComputername>D:
2. D:\>cd D:\PIRL\HUGO\pirl-docs-master\pirl-docs-master
3. Dir
4. Hugo.exe
5. Hugo.exe server
6. For shutting Hugo server down press: CTRL+C




### 3) Linux OS

J'ai créé deux méthodes possibles pour télécharger, installer et utiliser Hugo. Choisissez ce qui vous convient le mieux.
#### a) Installer par le gestionnaire de paquets

*Tapez la commande:
```
wget https://github.com/gohugoio/hugo/releases/download/v0.49/hugo_0.49_Linux-32bit.deb
sudo dpkg -i hugo_0.49_Linux-32bit.deb
```

#### b) Vous pouvez également installer via un script shell, puis utiliser un autre script pour faciliter le démarrage répétitif.
* Installation script

```
#!/bin/bash
wget https://github.com/gohugoio/hugo/releases/download/v0.49/hugo_0.49_Linux-64bit.tar.gz
tar -xf hugo_0.49_Linux-64bit.tar.gz
```
* Script de démarrage répétitif

```
#!/bin/bash
cd /path/to/hugo
ls -la
./hugo.sh &
pkill -f hugo.sh
./hugo.sh server
```
********************
## Vérification dans le navigateur Web

Lorsque votre installation est terminée, démarrez le navigateur Web et tapez:
```
http://localhost:1313
```
* Bienvenue dans la matrice. Vous pouvez maintenant modifier ou créer de nouveaux fichiers d'index et nous aider à créer un autre article basé sur la connaissance de l'étude.
* Choisissez pour cela l'éditeur de texte qui vous convient. Je préfère [Atom] (https://atom.io/). C’est vraiment facile à utiliser et convivial aussi avec GitLab.

--------

Author:
_[Mickey Maler](https://twitter.com/MickeyMaler)_

Contributor(s):
