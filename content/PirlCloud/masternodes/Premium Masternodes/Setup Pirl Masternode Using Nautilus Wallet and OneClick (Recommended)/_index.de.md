---
title: Setup Premium Masternode
weight: 1
pre: "<b>1. </b>"
chapter: true
---

{{< imagesurlsheaders "images_headers/Masternodes.png" >}}

- [Überblick](#overview)
- [Voraussetzungen](#prerequisites)
- [Poseidon Wallet Identitätsprüfung](#poseidon-wallet-identity-verification)
- [Nautilus Contract Ausführung](#nautilus-contract-execution)
- [Erstelle/Starte CentOS Linux Server](#create-launch-centos-linux-server)
- [Erstelle Masternode in Poseidon](#create-masternode-in-poseidon)
- [One-Click Masternode Setup](#one-click-masternode-setup)
- [Monitoring](#monitoring)

## Überblick

Zum Betreiben einer PIRL Masternode muss ein Virtual Private Server (VPS) mit einer statischen öffentlichen IP-Adresse verwendet werden, die einer Schnittstelle direkt   zugewiesen ist.

__*NAT (Adressübersetzung) ist nicht unterstützt.*__

Man sollte nur Pirl auf dem Server laufen lassen, andere Nodes oder irgendetwas können Konflikte verursachen!
In diesem Handbuch wird die Einrichtung der Masternode mit der One-Click Installation verwendet.
Diese Poseidon Funktion konfiguriert deinen CentOS 7 Linux Server automatisch als Pirl-Masternode.
Updates werden automatisch angewendet.
Du musst lediglich den Server überwachen, um sicherzustellen dass er betriebsbereit bleibt.
Dies alles ist einfach, wie zum Beispiel ein Neustart des Servers, sollte dieser offline gehen.

## Voraussetzungen

* **Ein VPS (CentOS 7 Linux) mit minimum 4GB RAM (mehr wird empfohlen), genügend Speicher um die Masternode auszuführen (mindestens 20 GB, empfohlen 60 GB +), eine statische öffentliche IP-Adresse, die direkt einer Schnittstelle zugewiesen ist.  NAT (Adressübersetzung) ist nicht unterstützt.**

 - Die offiziellen MINIMAL Anforderungen sind: 4GB RAM, 20GB Speicherplatz, 3TB Datenvolumen, öffentliche IPv4 Adresse.

 - Sobald du einen VPS bestellt hast, erhälst du in der Regel seine Root-Anmeldeinformationen. Am einfachsten ist es, diesen VPS nur für die Pirl Masternode zu verwenden und Poseidon die Root-Anmeldeinformationen zu geben, damit Poseidon den VPS verwalten und aktualisieren kann.

* **Einen Poseidon Account auf [https://poseidon.pirl.io](https://poseidon.pirl.io)**

 - Navigiere zu https://poseidon.pirl.io und registriere einen Account.  Denke daran dich mit deinem **USERNAME** anzumelden und nicht per E-Mail.

* **Nautilus Wallet**

 - Nautilus ist das offizielle Desktop Wallet für Pirl. Du benötigst es um die Funktion "Register Node" im Smart Contract auszuführen, was zum Registrieren und erfolgreichem Ausführen der Pirl Masternode erforderlich ist. Du kannst das Desktop Wallet verwenden um eine Pirl Adresse zu erstellen [Downloads Nautilus]({{< ref "/Downloads" >}}) oder du kannst das Web Wallet nutzen: https://wallet.pirl.io/.
 - Unabhängig von der Methode mit der du dein Wallet erstellst, sichere immer die UTC-Datei und das Kennwort!
 - Warnung: UTC Passwörter können nicht wiederhergestellt werden. Denken daran sich dieses zu merken, oder schreibe es auf!


* **20,001 Pirl verfügbar in deinem Wallet für eine Premium Masternode**

 - Daran führt kein Weg vorbei, es müssen zwanzigtausend PIRL in deinem Wallet stecken.
 - Und 1 oder 0,5 für Gas zum interagieren mit dem Smart Contract.
 - Du kannst Pirl Minen und einen der offiziellen Pools nutzen: https://pirl.io/en/pools/.
 - Oder du kannst Pirl an einer Börse erwerben. Empfohlen ist aktuell [https://www.stex.com](https://app.stex.com/de/trade/pair/BTC/PIRL/1D) als eine sichere und verlässliche Börse.

## Poseidon Wallet Identitätsprüfung

- Navigiere zu https://poseidon.pirl.io/ und login -> Navigiere zum Poseidon Wallet https://poseidon.pirl.io/dashboard/accounting/wallet/ und kopiere deine einzigartige Poseidon Wallet Addresse.

- Öffne dein Nautilus oder Web Wallet (Was auch immer du wählst und wo dein Stake gehalten werden soll) und sende 0.5 PIRL zu der Poseidon Wallet Address die im Schritt hiervor kopiert wurde.

- Sobald die Transaktion zur Bestätigung gesendet ist, navigiere zu https://explorer.pirl.network/ und füge deine Adresse in die Suchleiste. Die Suche zeigt dein Wallet und die entsprechende Transaktion an. -> Suchen die letzte Transaktion mit 0,5 PIRL von deinem Wallet zur Poseidon Wallet Adresse.

- Die erste Zeile des Transaktions-Blocks zeigt den Transaktions-Hash. Du brauchst diesen Hash-Wert später im Setup, um die Beziehung zwischen deinem Wallet mit dem Masternode Stake und dem Poseidon Wallet herzustellen.

![](https://i.imgur.com/tAWr8Ua.png)

> **Notiz:** Sende nicht mehr als 1 or 0.5 Pirl zur Verfifizierung an diese Adresse, dies ist NICHT die Adresse wo die 20000 Pirl hingesendet werden sollen, das kommt später.

Wenn du das Nautilus Wallet verwendest und auf die zuletzt gesendete Transaktion klickst, dann wird der Transaktions-Hash ebenfalls angezeigt. (Wird später noch mal gebraucht im Masternode TX-Hash Feld von Poseidon):

{{< imagesurlsheaders "cloud/txnautilus.png" >}}

## Nautilus Contract Ausführung

- **Öffne Nautilus** und navigiere zum **Contract** Reiter, zu finden in der rechten oberen Ecke.

![](https://cdn-images-1.medium.com/max/1600/0*OW_7W9P_u0k7ZdmZ.png)

- Sobald dort, klicke auf den **Watch Contract** Button.

![](https://cdn-images-1.medium.com/max/1600/0*wZbZlfAdjrUuhr53.png)

**In diesem Formular musst du ausfüllen:**

- **Premium MN:** Als **Contract Address** füge ein `0x256b2b26Fe8eCAd201103946F8C603b401cE16EC`. Der **Contract Name** für Premium Nodes, dies ist ein beliebiger String um diesen Contract zu identifizieren.

- Und zuletzt, das **JSON Interface Feld** muss mit folgendem Inhalt gefüllt werden:

```
[{"constant":false,"inputs":[],"name":"nodeRegistration","outputs":[{"name":"paid","type":"bool"}],"payable":true,"stateMutability":"payable","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getNodeAddress","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"","type":"address"}],"name":"moderators","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"","type":"address"}],"name":"nodes","outputs":[{"name":"pirlAddress","type":"address"},{"name":"nodeStake","type":"uint256"},{"name":"nodeHash","type":"bytes20"},{"name":"stakeLocked","type":"bool"},{"name":"nodeEnabled","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"disableNodeRegistration","outputs":[{"name":"disabled","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"nodeCost","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getStakeLockedStatus","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"nodeCount","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[{"name":"_admin","type":"address"}],"name":"setAdmin","outputs":[{"name":"set","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"owner","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"enableNode","outputs":[{"name":"enabled","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"nodeRegistrationEnabled","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"disableNode","outputs":[{"name":"disabled","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":false,"inputs":[],"name":"withdrawStake","outputs":[{"name":"withdrawn","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[{"name":"","type":"uint256"}],"name":"nodeAddresses","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getNodeEnabledStatus","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getNodeStake","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"enableNodeRegistration","outputs":[{"name":"enabled","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getNodeHash","outputs":[{"name":"","type":"bytes20"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"nodeFee","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"admin","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"inputs":[],"payable":false,"stateMutability":"nonpayable","type":"constructor"},{"payable":true,"stateMutability":"payable","type":"fallback"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_nodeRegistered","type":"bool"},{"indexed":false,"name":"_dateRegistered","type":"uint256"}],"name":"MasterNodeRegistered","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_nodeDisabled","type":"bool"},{"indexed":false,"name":"_dateDisabled","type":"uint256"}],"name":"MasterNodeDisabled","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_nodeEnabled","type":"bool"},{"indexed":false,"name":"_dateEnabled","type":"uint256"}],"name":"MasterNodeEnabled","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_nodePaid","type":"bool"},{"indexed":false,"name":"_datePaid","type":"uint256"}],"name":"MasterNodeRewarded","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_stakeWithdrawn","type":"bool"},{"indexed":false,"name":"_dateWithdrawn","type":"uint256"}],"name":"StakeWithdrawn","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_invoker","type":"address"},{"indexed":false,"name":"_dateEnabled","type":"uint256"},{"indexed":true,"name":"_registrationEnabled","type":"bool"}],"name":"MasterNodeRegistrationEnabled","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_invoker","type":"address"},{"indexed":false,"name":"_dateDisabled","type":"uint256"},{"indexed":true,"name":"_registrationDisabled","type":"bool"}],"name":"MasterNodeRegistrationDisabled","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_invoker","type":"address"},{"indexed":true,"name":"_admin","type":"address"},{"indexed":true,"name":"_adminSet","type":"bool"}],"name":"SetAdmin","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_invoker","type":"address"},{"indexed":true,"name":"_newOwner","type":"address"},{"indexed":true,"name":"_ownerChanged","type":"bool"}],"name":"TransferOwnership","type":"event"}]
```

- In the Contract section -> Select the contract that you just added and you will see the available functions as a dropdown menu on the right side under the **Write to Contract** heading.

- Under available functions select **Node Registration** and select the wallet containing your 20,000 Pirl for Premium MN.
Underneath that, fill in **20,000 Pirl** for Premium MN to send the stake to the contract.

![](https://cdn-images-1.medium.com/max/1600/0*eiHNFfmkEcgv5Szo.png)

- After selecting the wallet that contains the stake and select function **Node Registration** click **execute**, fill in your **UTC file password** and make sure you’re providing **at least 121,000 gas** for the transaction.

This is a good time to get some coffee or tea and let everything sync.  3-5 minutes should do the trick.

## Create/Launch CentOS Linux server

Verify that the server meets the appropriate specifications as noted in the:  
[Prerequisites](#prerequisites)  

- The server must run the CentOS 7 Linux distribution if you plan to use the **One-Click Masternode Setup**.

- Record of the static public IP address of the server as well as the root password.

Note: We do recommend logging into that server once to ensure the `root` credentials work.
It is not necessary to take any other actions on the server after that.
In fact, it's preferred that you don't make any other adjustments, at all.

## Create Masternode in Poseidon

- Login to Poseidon and navigate to the page which adds a masternode located here: https://poseidon.pirl.io/dashboard/masternodes/  
- Hit the plus button located at the right side of the page:  

![](https://i.imgur.com/N0rUi7z.jpg)

- Create Masternode pop-up will appear

{{< imagesurlsheaders "cloud/Create_Masternode_Record_in_Poseidon.PNG" >}}

- Name the masternoder with name of your choice.

- The Masternode Wallet id is the address of your Nautilus wallet, the one which contains 20,000 Pirl at present.

- Masternode TX hash - The transaction hash we saved earlier on at **Poseidon Wallet Identity Verification** step if the guide.

**On the bottom of the screenshot above, you will have to select that the MN is Premium (20K stake)**

Hit **Save changes** and then you will see the next screen.

{{< imagesurlsheaders "cloud/one_click_setup.PNG" >}}

## One-Click Masternode Setup

- Ensure that you know the public static IP address and `root` credentials before proceeding.

{{< imagesurlsheaders "cloud/one_click_setup.PNG" >}}

- Complete the fields -> SSH default is port: 22 Hit **Save changes** and then you will see the next screen.  

{{< imagesurlsheaders "cloud/Done.PNG" >}}

- After returning to the **My Masternodes** screen, observe that the masternode's **Managed by Poseidon** field is set to `True`

{{< imagesurlsheaders "cloud/managed.jpg" >}}

- Please allow 30 minutes for the process to complete. You may click the **details** button to monitor the status.

- Watch the masternode process synchronize with the blockchain:
```
journalctl -f
```

- Once messages like the following are displayed, your masternode is now synchronized and contributing to the network.

{{< imagesurlsheaders "cloud/vps.jpg" >}}

## Monitoring

We don't encourage active access on the server.  If, however, you wish to check the status, log into your server and issue the following command:
```
journalctl -f
```
your masternode is contributing to the network if it looks like this:.

{{< imagesurlsheaders "cloud/vps.jpg" >}}

Überwache den Status der Masternode, indem du auf die Poseidon Seite mit den Masternode Details klickst 🔍.
A functioning node should appear as follows:

{{< imagesurlsheaders "cloud/detailsmn.png" >}}

---
Author(s):

The Pirl Team

Contributor(s):

@Dptelecom
@packetflow
