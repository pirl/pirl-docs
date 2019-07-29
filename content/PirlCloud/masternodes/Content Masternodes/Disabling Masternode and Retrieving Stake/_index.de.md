---
title: Zurückerhalten des Masternode Stakes
weight: 2
pre: "<b>2. </b>"
chapter: true
---

{{< imagesurlsheaders "images_headers/Masternodes.png" >}}

## Überblick

Du kannst zu jeder Zeit zwei Masternode Smart Contract Funktionen ausführen und deinen Stake von 10.000 PIRL in dein Wallet zurückerhalten.

## Masternode deaktivieren und Stake zurückerhalten (Nautilus)

**Öffne Nautilus** und navigiere zum **Contract** Tab in der oberen rechten Ecke.

Du solltest den Masternode Contract auf der linken Seite sehen. Er hat die Adresse `0x6c042141C302C354509d2bff30EEFDEF24dE1047`. Selektiere die Adresse.

> **NOTIZ** Wenn der Contract bei dir unter **Watch Contract** nicht angezeigt wird, unten wird noch mal gezeigt wie er hinzugefügt wird.

Auf der rechten Seite werden die Contract Funktionen angezeigt.

Wähle die **Disable Node** Funktion aus, dann das Wallet, was in dem Contract als Masternode eingetragen ist und drücke **Execute**

<div align="center"><div style="width:55%;">{{< imagesurlsheaders "cloud/disable-node.png" >}}</div></div>

Stelle auf der nächsten Seite sicher das genug **Gas** für die Transaktion eingestellt ist, gebe dein **UTC-Datei Password** ein und drücke auf  **Send Transaction**.

<div align="center"><div style="width:55%;">{{< imagesurlsheaders "cloud/disable-node2.png" >}}</div></div>

Warte 30-60 Sekunden bevor du den nächsten Schritt ausführst.

Selektiere die **Withdraw Stake** Funktion, dann das Wallet, was in dem Contract als Masternode eingetragen ist und drücke **Execute**

<div align="center"><div style="width:55%;">{{< imagesurlsheaders "cloud/withdraw-stake.png" >}}</div></div>

Stelle auf der nächsten Seite sicher das genug **Gas** für die Transaktion eingestellt ist, gebe dein **UTC-Datei Password** ein und drücke auf  **Send Transaction**.

<div align="center"><div style="width:55%;">{{< imagesurlsheaders "cloud/disable-node2.png" >}}</div></div>

### Nicht genug Gas

Manchmal kann das Wallet das für eine Transaktion benötigte Gas nicht automatisch berechnen und setzt es automatisch auf 0. In diesem Fall kannst du das Gas manuell anpassen, indem du auf die Stelle mit der Aufschrift 0 klickst und einen Betrag eingibst. Eine gute Menge an Gas für diesen Zweck ist **121.000**.

<div align="center"><div style="width:55%;">{{< imagesurlsheaders "cloud/confirm-gas.png" >}}</div></div>

## Masternode Contract in Nautilus hinzufügen

**Öffne Nautilus** und navigiere um **Contract** Tab in der oberen rechten Ecke.

![](https://cdn-images-1.medium.com/max/1600/0*OW_7W9P_u0k7ZdmZ.png)

Sobald da, klicke auf den **Watch Contract** Button.

![](https://cdn-images-1.medium.com/max/1600/0*wZbZlfAdjrUuhr53.png)

Als **Contract Address** trage `0x6c042141C302C354509d2bff30EEFDEF24dE1047` ein. Und den **Contract Name** für Content Nodes, dies ist ein beliebiger String um diesen Contract zu identifizieren. 

Und zuletzt muss das **JSON Interface** Feld mit folgendem Inhalt gefüllt werden:

```
[{"constant":false,"inputs":[],"name":"nodeRegistration","outputs":[{"name":"paid","type":"bool"}],"payable":true,"stateMutability":"payable","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getNodeAddress","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"","type":"address"}],"name":"moderators","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"","type":"address"}],"name":"nodes","outputs":[{"name":"pirlAddress","type":"address"},{"name":"nodeStake","type":"uint256"},{"name":"nodeHash","type":"bytes20"},{"name":"stakeLocked","type":"bool"},{"name":"nodeEnabled","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"disableNodeRegistration","outputs":[{"name":"disabled","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"nodeCost","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getStakeLockedStatus","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"nodeCount","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[{"name":"_admin","type":"address"}],"name":"setAdmin","outputs":[{"name":"set","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"owner","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"enableNode","outputs":[{"name":"enabled","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"nodeRegistrationEnabled","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"disableNode","outputs":[{"name":"disabled","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":false,"inputs":[],"name":"withdrawStake","outputs":[{"name":"withdrawn","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[{"name":"","type":"uint256"}],"name":"nodeAddresses","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getNodeEnabledStatus","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getNodeStake","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"enableNodeRegistration","outputs":[{"name":"enabled","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getNodeHash","outputs":[{"name":"","type":"bytes20"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"nodeFee","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"admin","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"inputs":[],"payable":false,"stateMutability":"nonpayable","type":"constructor"},{"payable":true,"stateMutability":"payable","type":"fallback"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_nodeRegistered","type":"bool"},{"indexed":false,"name":"_dateRegistered","type":"uint256"}],"name":"MasterNodeRegistered","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_nodeDisabled","type":"bool"},{"indexed":false,"name":"_dateDisabled","type":"uint256"}],"name":"MasterNodeDisabled","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_nodeEnabled","type":"bool"},{"indexed":false,"name":"_dateEnabled","type":"uint256"}],"name":"MasterNodeEnabled","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_nodePaid","type":"bool"},{"indexed":false,"name":"_datePaid","type":"uint256"}],"name":"MasterNodeRewarded","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_stakeWithdrawn","type":"bool"},{"indexed":false,"name":"_dateWithdrawn","type":"uint256"}],"name":"StakeWithdrawn","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_invoker","type":"address"},{"indexed":false,"name":"_dateEnabled","type":"uint256"},{"indexed":true,"name":"_registrationEnabled","type":"bool"}],"name":"MasterNodeRegistrationEnabled","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_invoker","type":"address"},{"indexed":false,"name":"_dateDisabled","type":"uint256"},{"indexed":true,"name":"_registrationDisabled","type":"bool"}],"name":"MasterNodeRegistrationDisabled","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_invoker","type":"address"},{"indexed":true,"name":"_admin","type":"address"},{"indexed":true,"name":"_adminSet","type":"bool"}],"name":"SetAdmin","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_invoker","type":"address"},{"indexed":true,"name":"_newOwner","type":"address"},{"indexed":true,"name":"_ownerChanged","type":"bool"}],"name":"TransferOwnership","type":"event"}]

```

---
Author(s):

@Dptelecom

Contributor(s):

@packetflow
