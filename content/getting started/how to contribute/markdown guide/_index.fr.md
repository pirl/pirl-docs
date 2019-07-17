---
title: Guide Markdown
weight: 3
pre: "<b>3. </b>"
disableToc: true
---

## Introduction

Pour contribuer à la documentation PIRL, vous devrez utiliser ["markdown"](https://daringfireball.net/projects/markdown/syntax) mise en forme. Markdown est l’une des nombreuses façons de documenter. Ce n'est probablement pas le meilleur et certainement pas le pire. Il est facile d'entrer  et permet un cycle de documentation auto-cohérent.

Vous trouverez ci-dessous des exemples d'utilisation de Markdown, ainsi que nos recommandations et meilleures pratiques. Veuillez utiliser nos recommandations lors de la composition de la documentation PIRL afin que celle-ci soit bien assemblée avec le reste du contenu. Assurez-vous également de consulter le [Guide de style]({{< ref "/getting started/how to contribute/style guide" >}}) pour obtenir des instructions supplémentaires concernant le formatage du contenu.

##Exemple de document Markdown

Vous trouverez ci-dessous un exemple de document utilisant markdown. Ce document sera rendu par le logiciel pour afficher comme décrit.


{{< imagesurlsheaders "cloud/sample.jpg" >}}


## Basic Markdown Guide

### Titre principal

Le titre du document principal est affiché en haut du document en utilisant la police la plus grande. À démarquer, le titre se trouve tout en haut du document entre les deux. **`---`** section ci-dessous pour ce document.

```
---
title: Markdown Guide
weight: 5
---
```

### En-têtes

Les en-têtes sont généralement de H1 (le plus grand) à H6 (le plus petit). Markdown n'est pas différent. Le nombre représentant la taille de l'en-tête est représenté par un **`#`**. simple **`#`** est équivalent à **H1**, deux **`##`** is équivalent à ** H2 **, etc.
```
# This is an H1 tag
## This is an H2 tag
### This is an H3 tag
#### This is an H4 tag
##### This is an H5 tag
###### This is an H6 tag
```

> **PIRL TIP:** Les sections principales d’un document commencent par ** ## ** ou H2

### Accentuation

Pour * mettre en italique * le texte, utilisez un seul jeu d’astérisques autour de celui-ci. Pour marquer le texte en ** gras **, utilisez un ensemble de deux astérisques autour de celui-ci. Pour supprimer un texte, utilisez deux tildes ** (~) ** autour de celui-ci.

```
*This text will be italicized*
**This text will be in bold**
_**What about bold italic**_
~~Did I say something wrong?~~
<center>I am centered writer</center>
```

*Ce texte sera en italique *

** Ce texte sera en gras **

_ ** Qu'en est-il du gras italique ** _

~~ Ai-je dit quelque chose de mal? ~~

<center> Je suis un écrivain centré </ center>

### Citation

Pour citer quelque chose, utilisez un crochet droit> Et faites votre devis!
```
>**Manual to this article**: You have to read this article from front to back and show your grace. After all, that is how literature works, right?
(unless it is instruction manual, in which case no one reads them at all)
```
>**Manuel de cet article **: Vous devez lire cet article de haut en bas et montrer votre grâce. Après tout, c'est comme ça que la littérature fonctionne, non?
(sauf s'il s'agit d'un manuel d'instructions, auquel cas personne ne les lit du tout)

### Table
Si vous voulez créer un tableau simple dans l'éditeur de texte Atom, vous pouvez simplement chronométrer "tableau" et appuyer sur un bouton Entrée! Si vous écrivez dans le bloc-notes, eh bien,
alors je souhaite de sincères condoléances :) Mais en écrivant ces symboles, vous pouvez créer une seule ligne et une seule colonne.

Ici vous avez deux exemples:


```
| Header One     | Header Two     |
| :------------- | :------------- |
| Item One       | Item Two       |
```
| Header One     | Header Two     |
| :------------- | :------------- |
| Item One       | Item Two       |



```
|[Web page](https://pirl.io/)|[White Paper](https://storage.gra1.cloud.ovh.net/v1/AUTH_33a0c4ac73cf4d88a243480c275be8ac/pirl/pirl-whitepaper.pdf)| [Twitter](https://twitter.com/PirlOfficial)  |
|:------------- |:-------------:| -----:|

```
|[Web page](https://pirl.io/)|[White Paper](https://storage.gra1.cloud.ovh.net/v1/AUTH_33a0c4ac73cf4d88a243480c275be8ac/pirl/pirl-whitepaper.pdf)| [Twitter](https://twitter.com/PirlOfficial)  |
|:------------- |:-------------:| -----:|



### Des listes

Les listes ordonnées sont créées en utilisant ** 1. ** pour l'élément de recherche, puis en s'incrémentant à chaque ligne suivante. Les listes non ordonnées sont créées à l'aide de ** + **.
```
1. First
2. Second
3. Third

+ Satoshi
+ Vitalik
+ PIRL

1. This is first
  + First thing
2. This is Second
  + Second thing
3. This is Third
  + Third thing
```

1. First
2. Second
3. Third

+ Satoshi
+ Vitalik
+ PIRL

1. This is first
  + First thing
2. This is Second
  + Second thing
3. This is Third
    + Third thing

### Links

Faire des liens consiste simplement à coller un URL entre un ensemble de parenthèses ** () **. Il y a aussi quelques options supplémentaires.

```
This is an [example link](http://example.com/ "With a Title"). It will still work if the only thing included is the link within the parenthesis.
```

Ceci est un [exemple de lien](http://example.com/ "Avec un titre "). Cela fonctionnera toujours si la seule chose incluse est le lien dans la parenthèse.

### Images


Lier des images, c'est comme des liens avec un shortcode {{< imagesurlsheaders "cloud/magic.gif" >}}

```
* {{< imagesurlsheaders "cloud/magic.gif" >}}
```

* {{< imagesurlsheaders "cloud/magic.gif" >}}


### Code

Il existe deux manières de distinguer le code du texte: une pour l'utilisation en ligne et l'autre pour les blocs de code. Distinguer le code `inline` mettre une série de backticks autour de lui. Pour le faire comme un bloc de texte, mettez trois backticks au tom et au bas.

{{< imagesurlsheaders "cloud/code.jpg" >}}


```
This is will be displayed a as a block of code.
More importantly, notice the back ticks at the top and bottom.
```

---
Author:
_[PrimateCrypto](https://twitter.com/PrimateCrypto)_


Contributor(s):  

@dptelecom
