---
title: PirlGuard
weight: 6
pre: "<b>6. </b>"
chapter: true
---

{{< imagesurlsheaders "images_headers/pirlguard.png"  >}}


## PirlGuard - Solution innovante contre une attaques 51%

<iframe width="560" height="315" src="https://www.youtube.com/embed/Q-f01eFYlig" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


Pirl block 2,442,442 est un événement historique non seulement pour Pirl mais pour la sécurité de la blockchain en général.

Comme la plupart des membres de la communauté Pirl le savent, l’équipe Pirl étudie depuis plusieurs mois différentes manières de sécuriser notre blockchain contre les attaques ASICS et 51%, dans notre discorde et dans les coulisses. Au cours de cette période, Pirl a été victime d’une attaque  51% avec beaucoup d’autres blockchains.



{{< imagesurlsheaders "cloud/1.png" >}}




L’un des facteurs de menace qui a récemment rendu presque tous les Blockchains du mécanisme de consensus du PoW susceptibles d’être attaqués à 51% est le recul des bénéfices miniers, ce qui a entraîné une surconsommation d’énergie de hachage à bas prix.


La plupart des sources disponibles expliquent la complexité de ces attaques et présentent les solutions PoS et tierces comme une bonne mesure de protection contre de telles attaques. Une solution consisterait à supprimer la blockchain, ce qui nuirait toujours aux mineurs, aux investisseurs et aux détenteurs de Pirl. Même si un mécanisme de consensus de point de vente est également vulnérable, d’autres types d’attaques, telles que l’attaque «Nothing-In-Stake».


Après une recherche et une analyse approfondies des méthodes de sécurité de  la blockchain, l’équipe Pirl n’a considéré aucune des options actuellement disponibles comme une mesure acceptable évitable à long terme contre ce type d’attaque. Cela laissait à l'équipe le seul choix possible pour développer un nouveau protocole de sécurité.


Afin de comprendre le protocole PirlGuard, notamment comment et pourquoi le développement de la solution innovante par Pirl, vous devez comprendre le fonctionnement d’une attaque  51%. Si vous avez confiance en vos connaissances en matière d'anatomie d'une attaque  51%, n'hésitez pas à passer à la section «Comment fonctionne PirlGuard?» De cet article.


## Comment fonctionne une attaque  51%


Source: [CoinMonks](https://medium.com/coinmonks/what-is-a-51-attack-or-double-spend-attack-aa108db63474)


Author: [Jimi.S](https://twitter.com/JimiSinnige)


Lorsqu'un propriétaire de Bitcoin approuve une transaction, celle-ci est placée dans un pool local de transactions non confirmées. Les mineurs sélectionnent les transactions à partir de ces pools pour former un bloc de transactions. Afin d’ajouter ce bloc de transactions à la blockchain,
ils doivent trouver une solution à un problème mathématique très difficile. Ils essaient de trouver cette solution en utilisant la puissance de calcul. Ceci est appelé hachage.
Plus un mineur dispose de capacités de calcul, meilleures sont ses chances de trouver une solution avant que les autres mineurs ne trouvent la leur. Quand un mineur trouve une solution,
il sera diffusé (avec son bloc) aux autres mineurs et ceux-ci ne le vérifieront que si toutes les transactions à l'intérieur du bloc sont valides conformément à l'enregistrement existant des transactions sur la blockchain.
Notez que même un mineur corrompu ne peut jamais créer de transaction pour quelqu'un d'autre car il aurait besoin de la signature numérique de cette personne pour le faire (sa clé privée).
Envoi de Bitcoin à partir du compte d’une autre personne est donc tout simplement impossible sans l’accès à la clé privée correspondante.


## Exploitation minière furtive - création d'une progéniture de la blockchain


Maintenant, faites attention. Un mineur malveillant peut toutefois essayer d’annuler les transactions existantes. Lorsqu'un mineur trouve une solution, celle-ci est censée être diffusée à tous les autres mineurs afin qu'ils puissent la vérifier, après quoi le bloc est ajouté à la blockchain (les mineurs parviennent à un consensus). Cependant, un mineur corrompu peut créer une descendance de la blockchain en ne diffusant pas les solutions de ses blocs au reste du réseau. Il existe maintenant deux versions de la blockchain.



{{< imagesurlsheaders "cloud/2.png" >}}



Il existe maintenant deux versions de la blockchain. La blockchain rouge peut être considérée en mode ‘furtif’.

Une version qui est suivie par les mineurs non corrompus, et une qui est suivie par le mineur corrompu. Le mineur corrompu travaille actuellement sur sa propre version de cette blockchain et ne la diffuse pas sur le reste du réseau. Le reste du réseau ne capte pas cette chaîne car, après tout, elle n’a pas été diffusée. Il est isolé du reste du réseau. Le mineur corrompu peut désormais dépenser tous ses Bitcoins sur la version véridique de la blockchain, celle sur laquelle travaillent tous les autres mineurs. Disons qu’il depense pour une Lamborghini. Sur la chaîne de blocs en vérité, ses Bitcoins sont maintenant épuisés. En attendant, il n'inclut pas ces transactions dans sa version isolée de la blockchain. Sur sa version isolée de la blockchain, il a encore ces Bitcoins.



{{< imagesurlsheaders "cloud/3.png" >}}


Pendant ce temps, il ramasse toujours des blocs et il les vérifie tous seuls sur sa version isolée de la blockchain. C'est là que tout problème commence… La blockchain est programmée pour suivre un modèle de gouvernance démocratique, autrement dit la majorité. La blockchain le fait en suivant toujours la chaîne la plus longue. Après tout, la majorité des mineurs ajoutent des blocs à leur version de la blockchain plus rapidement que le reste du réseau (donc; la plus longue chaîne = majorité). C'est ainsi que la blockchain détermine quelle version de sa chaîne est la vérité et, en retour, sur quoi sont basés tous les soldes de portefeuilles. Une course a maintenant commencé. Celui qui a le plus de puissance de hachage ajoutera des blocs à sa version de la chaîne plus rapidement.



{{< imagesurlsheaders "cloud/4.png" >}}



##Une course - inverser les transactions existantes en diffusant une nouvelle chaîne


Le mineur corrompu va maintenant essayer d’ajouter des blocs à sa blockchain isolée plus rapidement que les autres mineurs d’ajouter des blocs à leur blockchain (la chaîne véridique). Dès que le mineur corrompu crée une blockchain plus longue, il diffuse soudainement cette version de la blockchain vers le reste du réseau. Le reste du réseau va maintenant détecter que cette version (corrompue) de la blockchain est en réalité plus longue que celle sur laquelle elle travaillait, et le protocole les oblige à basculer sur cette chaîne.



{{< imagesurlsheaders "cloud/5.png" >}}


La blockchain corrompue est maintenant considérée comme la blockchain véridique et toutes les transactions qui ne sont pas incluses dans cette chaîne seront immédiatement annulées. L’attaquant a déjà dépensé ses Bitcoins sur une Lamborghini, mais cette transaction n’était pas incluse dans sa chaîne furtive, la chaîne qui est maintenant sous contrôle, et il contrôle donc à nouveau ces bitcoins. Il est capable de les dépenser à nouveau.



{{< imagesurlsheaders "cloud/6.png" >}}



* Ceci est une attaque à double dépense. *
Il est communément appelé une attaque  51%, car le mineur malveillant aura besoin de plus de puissance de hachage que le reste du réseau combiné (donc 51% de la puissance de hachage) afin d’ajouter des blocs à sa version de la blockchain plus rapidement, permettant finalement lui de construire une chaîne plus longue.


Maintenant que nous savons comment fonctionne l'attaque, nous pouvons la résumer en quelques moments clés.


A) L'attaquant doit exploiter sa propre version de la blockchain en privé avec un hashrate supérieur à celui du réseau principal afin d'être plus rapide et de créer une chaîne plus longue. C'est souvent une course pour obtenir une chaîne de 10-20-50 blocs de plus.


B) Une fois qu'il est en possession d'une blockchain plus longue, il doit la diffuser sur le réseau. Ensuite, le réseau doit reconnaître la chaîne la plus longue et l'accepter.


C) Une double dépense réussie rendrait orpheline les transactions initiales rendant les pièces disponibles dans le portefeuille de l'attaquant une fois de plus après la longue chaîne appliquée.


## Comment fonctionne PirlGuard?


Afin de perturber les mécanismes derrière l'attaque  51% permettant à un attaquant de réussir, nous avons déployé une solution centrale avec un algorithme de consensus modifié qui défendra dans un avenir proche notre blockchain et de nombreuses autres contre la quasi-totalité des attaques.


## PirlGuard System
Avec le protocole PirlGuard déployé, les chances de réussite d'une attaque sont considérablement réduites. Comme nous le savons, une fois que l'attaquant a créé une chaîne plus longue en exploitant en privé une chaîne distincte, il doit ensuite la diffuser sur le réseau. Une fois que l'attaquant a ouvert son nœud pour le faire apparaitre , il tentera de relier les autres nœuds du réseau en leur indiquant qu'ils ont tort. Cependant, une fois que cela se produira, PirlGuard abandonnera le pair et le pénalisera en le condamnant à une amende correspondant à X blocs de pénalités en raison de son extraction non comparée. Le nombre de blocs de pénalité attribués dépend du nombre de blocs que le mineur malveillant a exploités en privé.



{{< imagesurlsheaders "cloud/7.png" >}}


Le protocole de sécurité PirlGuard dissuade beaucoup les attaquants d’essayer d’effectuer un peering malveillant, ce qui donne au réseau principal un coup de fouet indispensable en matière de sécurité. Ce nouveau mécanisme de sécurité réduit les chances à environ 0,03%.


Mais ce n’est pas la seule mesure de sécurité que nous avons préparée.


## Contrats de notaire exploités par Masternode sur plusieurs blockchains et système de surveillance.


Les masternodes assumeront un nouveau rôle avec leurs autres fonctions d’utilité. Ils vont notariser la blockchain et seront autorisés à agir dans le processus de pénalisation des mauvais acteurs et à préserver un consensus honnête sur la blockchain de Pirl.

Au cas où un attaquant serait toujours déterminé à utiliser une grande quantité de fonds et de ressources pour tenter sa chance (0,03% de chance) et parviendrait en quelque sorte à imposer une chaîne plus longue sur le réseau, un système de surveillance orphelin nouvellement initialisé détectera les réorganisations de blocs orphelins. qui alertera l'équipe pour qu'elle prenne les mesures et contre-mesures nécessaires.


À titre de mesure de sécurité supplémentaire, le contrat de notaire sera déployé à la fois sur les chaînes de blocs Pirl et Ethereum.


## Augmenter le nombre de confirmations requises pour les échanges.


Une mesure supplémentaire qui sera mise en œuvre est une exigence plus élevée de confirmation de bloc sur les échanges pour valider les dépôts. Une autre étape pour rendre une attaque presque impossible et ne vaut même pas le temps d'un attaquant.

##  Open Source


Jusqu'à présent, Pirl a contribué à la création de la blockchain en développant le premier réseau de masternode basé sur du code Ethash, la première implémentation IPFS privée fonctionnant sur un réseau de masternode.
Le protocole de sécurité PirlGuard sera ajouté à notre bibliothèque open source avec le cœur du projet.
Chez Pirl, nous développons pour révolutionner et rationaliser la technologie de blockchain pour l’ensemble du secteur des blockchain. Cela signifie que notre code sera disponible pour quiconque pourra étudier, éduquer, tester, modifier ou appliquer sa propre sécurité réseau blockchain contre de futures attaques  51%.


[Source Code:](https://git.pirl.io/community/pirl)
[Website:](https://pirl.io/en)






#PirlTogetherStrong


Votre,

Equipe Pirl


---
Author(s):  


@Fawkes

Contributor():


@dptelecom
