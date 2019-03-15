---
title: Installation Premium Masternode
weight: 1
pre: "<b>1. </b>"
chapter: true
---
{{< imagesurlsheaders "images_headers/Masternodes.png" >}}

- [Vue d’ensemble](#vue-d-ensemble)
- [Conditions préalables](#conditions-pr-alables)
- [Vérification d'identité de portefeuille Poseidon](#v-rification-d-identit--de-portefeuille-poseidon)
- [Exécution du contrat Nautilus](#ex-cution-du-contrat-nautilus)
- [Créer / lancer un serveur Linux CentOS](#cr-er---lancer-un-serveur-linux-centos)
- [Créer un masternode sur Poseidon](#cr-er-un-masternode-sur-poseidon)
- [Configuration du masternode en un clic](#configuration-du-masternode-en-un-clic)
- [Surveillance](#surveillance)  



## Vue d’ensemble

L'exécution d'un nœud  masternode PIRL nécessite l'utilisation d'un serveur privé virtuel (VPS) avec une adresse IP publique statique directement affectée à une interface.  
*NAT (traduction d'adresse) n'est pas pris en charge*


Avoir seulement pirl en cours d'exécution sur le serveur, pas d'autres nœuds ou quoi que ce soit, cela causerait un conflit !!  
Une fois les fonds en place, vous envoyez une petite transaction 1 PIRL sur votre portefeuille Poseidon (votre compte sera accompagné d’un portefeuille) pour prouver que vous contrôlez le portefeuille Nautilus avec le capital de 20K PIRL pour Premium MN.  
Vous utilisez l'identifiant txid de la transaction 1 PIRL dans la configuration du masternode, avec votre adresse Nautilus.  
Lorsque le masternode est ajouté, vous retournez dans votre portefeuille Nautilus et ajoutez l'adresse du contrat du masternode dans l'onglet «contrats».  
Avec l'adresse de contrat masternode en place, vous exécutez la fonction d'enregistrement de nœud.  
À ce stade, vous pouvez utiliser la fonctionnalité One-Click de Poseidon pour configurer automatiquement votre serveur et le maintenir à jour.  


Ce guide utilise la fonction de configuration en un seul clic.  
Cette fonction Poseidon configure automatiquement votre serveur linux CentOS 7 pour qu’il soit un Masternode Pirl.  
Les mises à jour seront appliquées automatiquement.  
Tout ce que vous avez à faire est de surveiller votre serveur pour s’assurer qu’il reste opérationnel.  
C’est aussi simple que de redémarrer le serveur, si celui-ci est déconnecté


## Conditions préalables

* **Un VPS avec au moins 4 Go de mémoire RAM totale du système d'exploitation minimum (plus est recommandé), suffisamment de mémoire pour exécuter le masternode (minimum 20 Go, recommandé 60 Go +) et une adresse IP publique statique assignée directement à une interface. NAT (traduction d'adresse) n'est pas pris en charge.**
 - Les exigences officielles MINIMUM sont: 4 GB de RAM, 20 GB d’espace, 3 TB de transfert, IPv4 IP public. Une fois que vous commandez votre VPS, vous recevrez ces informations d'identification Root. Le chemin le plus simple consiste à utiliser ce VPS uniquement pour votre Pirl Masternode et donner à Poseidon vos informations d'identification Root afin qu'il puisse gérer et mettre à jour votre VPS.  
* **Un compte Poseidon sur  [https://poseidon.pirl.io](https://poseidon.pirl.io)**  
 - Accédez à https://poseidon.pirl.io et créer un compte. Garder à l'esprit que vous vous connecterez avec votre nom d'utilisateur et non par email.  
* **Portefeuille Nautilus**  
 - Nautilus est le portefeuille de bureau officiel de Pirl. Vous en aurez besoin pour ajouter et exécuter «Register Node» à partir du contrat intelligent requis pour exécuter le masternode Pirl. Vous pouvez utiliser le portefeuille de bureau pour créer votre portefeuille Pirl [Downloads Nautilus]({{< ref "/Downloads" >}}) ou vous pouvez utiliser le portefeuille Web à l'adresse: https://wallet.pirl.io/.  
 - Quelle que soit la méthode choisie pour créer votre portefeuille, veillez toujours à enregistrer votre fichier UTC.  
 - le mot de passe nécessaire pour décrypter le fichier UTC ainsi que votre clé privée.   
 - Vous pouvez utiliser votre fichier UTC et votre mot de passe créés par Nautilus pour extraire votre clé privée.  
 - YVous pouvez utiliser votre clé privée au lieu du fichier UTC + Mot de passe pour accéder à votre portefeuille et retirer vos fonds en cas d’urgence.  
* **20 001 Pirl disponibles dans votre portefeuille pour Premium MN**
 - Il n’y a aucun moyen de s’en sortir, vous devrez d’une manière ou d’une autre placer vingt mille PIRL dans un portefeuille.  
 - 1 ou 0,5 pour que le gaz interagisse avec le contrat.  
 - Vous pouvez exploiter Pirl en utilisant l’un des pools officiels disponibles ici: https://pirl.io/en/pools/.  
 - Vous pouvez également acheter Pirl sur l'un des échanges Pirl. Je recommande https://www.stex.com comme échange sûr et fiable.


## Vérification d'identité de portefeuille Poseidon  

La première étape du processus de configuration du masternode consiste à envoyer une transaction de votre portefeuille Nautilus (vous pouvez également utiliser le portefeuille Web ici si nécessaire) vers votre portefeuille Poseidon situé ici:  https://poseidon.pirl.io/dashboard/accounting/wallet/.  
This is just like sending Pirl to any other wallet, except in this case it’s your unique Poseidon wallet.  
C’est comme si vous envoyez Pirl dans n’importe quel autre portefeuille, sauf que c’est votre unique portefeuille Poseidon.  
Cela prouve à Poseidon que vous contrôlez votre portefeuille Nautilus.  
N'envoyez plus 1 ou .5 pirl à cette adresse pour vérification, ce n'est pas l'adresse à laquelle vous enverrez les 20 000 pirls.  
cela vient plus tard.


Accédez à https://poseidon.pirl.io/ et collez votre adresse  portefeuille Nautilus en haut.  
Ceci affichera toutes les transactions entrant et sortant de votre portefeuille Nautilus.  
La dernière transaction sortante montrera qu’elle se connecte à l’adresse de votre portefeuille Poseidon.  
Tout à gauche de la page, le txid (c'est-à-dire le hachage de transaction) sera affiché.  
Ou Dans le portefeuille Nautilus, vous cliquez une fois sur la transaction envoyée et vous voyez ce Tx-id:  
Prenez et sécurisez ce txid et copiez-le, car vous en aurez besoin plus tard.


**TRES IMPORTANT: Il y a 2 hashes pour chaque transaction.  
Il y a le hash de transaction (txid) et le hash de bloc.  
Vous devez utiliser le hachage de transaction (txid) pour que le processus de configuration du masternode fonctionne.  
Il existe un moyen très simple de savoir lequel est le txid.  
Le txid se trouve à gauche de la liste des transactions générales de votre portefeuille.  
Une fois que vous avez cliqué sur le txid lui-même, vous verrez le bloc hachage affiché.  
Ne pas utiliser le hash du bloc.  
Utilisez le txid situé du côté gauche de la liste des transactions de votre portefeuille sur Poseidon.**  

![](https://cdn-images-1.medium.com/max/1600/0*1LTQiVdFomhRei6u.png)
![](https://cdn-images-1.medium.com/max/1600/0*bVaXgKomLeN0mEYQ.png)


Dans le portefeuille Nautilus, vous cliquez une fois sur la transaction envoyée et vous voyez ce Tx-id:

{{< imagesurlsheaders "cloud/txnautilus.png" >}}



## Exécution du contrat Nautilus  

Maintenant nous avons la partie la plus difficile à résoudre, passons à Nautilus et ajoutons le contrat Pirl Masternode.  

**Ouvrez Nautilus** et accédez à l'onglet **Contrat** situé dans le coin supérieur droit.  

![](https://cdn-images-1.medium.com/max/1600/0*OW_7W9P_u0k7ZdmZ.png)

Une fois là-bas, cliquez sur le bouton **Watch Contract**.  

![](https://cdn-images-1.medium.com/max/1600/0*wZbZlfAdjrUuhr53.png)


Il existe deux contrats 1 pour chaque type de noeud,  
le JSON est identique pour tous les Masternodes


**Premium MN:** pour **l'adresse du contrat** renseignez `0x256b2b26Fe8eCAd201103946F8C603b401cE16EC`.
Le **nom du contrat** pour ce nom est premium même s'il peut être ce que vous voulez.
Enfin,  
**le champ Interface JSON** doit être renseigné avec:  


```
[{"constant":false,"inputs":[],"name":"nodeRegistration","outputs":[{"name":"paid","type":"bool"}],"payable":true,"stateMutability":"payable","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getNodeAddress","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"","type":"address"}],"name":"moderators","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"","type":"address"}],"name":"nodes","outputs":[{"name":"pirlAddress","type":"address"},{"name":"nodeStake","type":"uint256"},{"name":"nodeHash","type":"bytes20"},{"name":"stakeLocked","type":"bool"},{"name":"nodeEnabled","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"disableNodeRegistration","outputs":[{"name":"disabled","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"nodeCost","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getStakeLockedStatus","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"nodeCount","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[{"name":"_admin","type":"address"}],"name":"setAdmin","outputs":[{"name":"set","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"owner","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"enableNode","outputs":[{"name":"enabled","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"nodeRegistrationEnabled","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"disableNode","outputs":[{"name":"disabled","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":false,"inputs":[],"name":"withdrawStake","outputs":[{"name":"withdrawn","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[{"name":"","type":"uint256"}],"name":"nodeAddresses","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getNodeEnabledStatus","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getNodeStake","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"enableNodeRegistration","outputs":[{"name":"enabled","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getNodeHash","outputs":[{"name":"","type":"bytes20"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"nodeFee","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"admin","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"inputs":[],"payable":false,"stateMutability":"nonpayable","type":"constructor"},{"payable":true,"stateMutability":"payable","type":"fallback"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_nodeRegistered","type":"bool"},{"indexed":false,"name":"_dateRegistered","type":"uint256"}],"name":"MasterNodeRegistered","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_nodeDisabled","type":"bool"},{"indexed":false,"name":"_dateDisabled","type":"uint256"}],"name":"MasterNodeDisabled","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_nodeEnabled","type":"bool"},{"indexed":false,"name":"_dateEnabled","type":"uint256"}],"name":"MasterNodeEnabled","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_nodePaid","type":"bool"},{"indexed":false,"name":"_datePaid","type":"uint256"}],"name":"MasterNodeRewarded","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_stakeWithdrawn","type":"bool"},{"indexed":false,"name":"_dateWithdrawn","type":"uint256"}],"name":"StakeWithdrawn","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_invoker","type":"address"},{"indexed":false,"name":"_dateEnabled","type":"uint256"},{"indexed":true,"name":"_registrationEnabled","type":"bool"}],"name":"MasterNodeRegistrationEnabled","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_invoker","type":"address"},{"indexed":false,"name":"_dateDisabled","type":"uint256"},{"indexed":true,"name":"_registrationDisabled","type":"bool"}],"name":"MasterNodeRegistrationDisabled","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_invoker","type":"address"},{"indexed":true,"name":"_admin","type":"address"},{"indexed":true,"name":"_adminSet","type":"bool"}],"name":"SetAdmin","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_invoker","type":"address"},{"indexed":true,"name":"_newOwner","type":"address"},{"indexed":true,"name":"_ownerChanged","type":"bool"}],"name":"TransferOwnership","type":"event"}]
```



Sélectionnez le nouveau contrat Masternode et vous verrez les fonctions disponibles sous forme de menu déroulant à droite sous l'en-tête Write to Contract.  
Sous Fonctions disponibles, sélectionnez **Node Registration** et sélectionnez le portefeuille contenant vos 20 000 Pirl pour Premium MN.  
En dessous, remplissez **20 000 Pirl** pour Premium MN afin d’envoyer la mise au contrat.  

![](https://cdn-images-1.medium.com/max/1600/0*eiHNFfmkEcgv5Szo.png)

Une fois que vous avez  **exécuté**, entrez le mot de passe de votre **fichier UTC** et assurez-vous que vous fournissez **au moins 121 000 GAZ** pour la transaction.   

C'est un bon moment pour prendre un café ou un thé et laisser tout se synchroniser.  3-5 minutes devraient faire l’affaire.  


## Créer / lancer un serveur Linux CentOS  


Vérifiez que le serveur répond aux spécifications appropriées indiquées dans  [Pirl Masternode Setup Tutorial](https://pirl.io/blog/1-pirl-masternode-setup-tutorial)

si vous envisagez d’utiliser la configuration  **masternode en un clic**.  
Le serveur doit exécuter la distribution Linux CentOS 7.  

Enregistrement de l'adresse IP publique statique du serveur ainsi que du mot de passe root.  
Nous vous recommandons de vous connecter une fois sur ce serveur pour vous assurer que les informations d’identification Root fonctionnent.  
Il n'est pas nécessaire de faire d'autres actions sur le serveur après cela.  
En fait, il est préférable de ne faire aucun autre ajustement.  


## Créer un masternode sur Poseidon  

Connectez-vous à Poseidon et accédez à la page qui ajoute un masternode situé ici:  
https://poseidon.pirl.io/dashboard/masternodes/  
et appuyez sur le:  


{{< imagesurlsheaders "cloud/redcrossadd.jpg" >}}


alors vous obtenez ce joli écran:  

{{< imagesurlsheaders "cloud/Create_Masternode_Record_in_Poseidon.PNG" >}}


Le nom peut être ce que vous voulez.  
Le numéro de portefeuille Masternode est l'adresse de votre portefeuille Nautilus, celui qui contient actuellement 20 000 Pirl.  
Et rappelez-vous,  
le champ de validation du hachage Tx a besoin du txid (pas du hachage de bloc voir ci-dessus!)  
De la transaction que vous envoyez à votre portefeuille Poseidon.  


**Au bas de la capture d'écran ci-dessus, vous devrez sélectionner le MN comme Premium (20K stake)**  

Appuyez **sur Enregistrer les modifications** pour afficher l'écran suivant.  

{{< imagesurlsheaders "cloud/one_click_setup.PNG" >}}




## Configuration du masternode en un clic

Assurez-vous de connaître l'adresse IP statique publique et les informations d'identification Root avant de poursuivre.  


{{< imagesurlsheaders "cloud/one_click_setup.PNG" >}}


nous allons compléter tous les champs.  
ssh par défaut est le port: 22 Appuyez sur Enregistrer les modifications,  
puis l'écran suivant s'affichera  

{{< imagesurlsheaders "cloud/Done.PNG" >}}


Après être revenu à l'écran **My masternodes**, observez que le champ **Géré par Poseidon du masternode** est défini sur `True`  

{{< imagesurlsheaders "cloud/managed.jpg" >}}

Veuillez prévoir 30 minutes pour que le processus se termine. Vous pouvez cliquer sur le bouton **Détails** pour surveiller le statut.  

Regardez le processus de masternode se synchroniser avec la blockchain:  

```
journalctl -f
```

Une fois que les messages suivants sont affichés, votre masternode est maintenant synchronisé et contribue au réseau.  


{{< imagesurlsheaders "cloud/vps.jpg" >}}




## Surveillance  

Nous n’encourageons pas l’accès actif sur le serveur. Si, toutefois, vous souhaitez vérifier l'état, connectez-vous à votre serveur et exécutez la commande suivante:  
```
journalctl -f
```
votre masternode contribue au réseau s'il ressemble à ceci:  


{{< imagesurlsheaders "cloud/vps.jpg" >}}


Surveillez l’état de votre masternode en consultant la page Détails du masternode Poseidon en cliquant sur le bouton.  
Un nœud en fonctionnement devrait apparaître de la façon suivante:  


{{< imagesurlsheaders "cloud/detailsmn.png" >}}




---
Author(s):


The Pirl Team


Contributor(s):


@Dptelecom  
@ClaudioPirl
