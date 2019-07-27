---
title: Setup Premium Masternode
weight: 1
pre: "<b>1. </b>"
chapter: true
---

{{< imagesurlsheaders "images_headers/Masternodes.png" >}}

- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Poseidon Wallet Identity Verification](#poseidon-wallet-identity-verification)
- [Nautilus Contract Execution](#nautilus-contract-execution)
- [Create/Launch CentOS Linux server](#create-launch-centos-linux-server)
- [Create Masternode in Poseidon](#create-masternode-in-poseidon)
- [One-Click Masternode Setup](#one-click-masternode-setup)
- [Monitoring](#monitoring)

## Overview

Running a PIRL masternode requires the use of a Virtual Private Server (VPS) with a static public IP address directly assigned to an interface.

__*NAT (address translation) is not supported.*__

One should only have Pirl running on the server, any other nodes or anything else will cause a conflict!

This guide uses the one-click-masternode setup feature.
This Poseidon feature automatically configures your CentOS 7 linux server to be a Pirl Masternode.
Updates will be applied automatically.
All you have to do is monitor your server to ensure it stays operational.
This is as simple as rebooting the server, should it go offline.

## Prerequisites

* **A VPS (CentOS 7 Linux) with minimum 4GB Total OS RAM minimum (more is recommended), enough storage to run the masternode (Minimum 20GB, Recommended 60GB+), and a static public IP address directly assigned to an interface.  NAT (address translation) is not supported.**

 - The official MINIMUM requirements are: 4GB RAM, 20GB space, 3TB transfer, public IPv4 IP.

 - Once you order your VPS, you will receive its root credentials. The easiest path forward is to only use this VPS for your Pirl Masternode and give Poseidon your root credentials so it can manage and update your VPS.

* **A Poseidon account on [https://poseidon.pirl.io](https://poseidon.pirl.io)**

 - Navigate over to https://poseidon.pirl.io and register for an account.  Keep in mind that you will be logging in with your **USERNAME** and not email.

* **Nautilus wallet**

 - Nautilus is the official desktop wallet for Pirl.  You will need it in order to add and execute “Register Node” from the smart contract needed to run the Pirl masternode.  You can use the desktop wallet to create your Pirl wallet [Downloads Nautilus]({{< ref "/Downloads" >}}) or you can use the web wallet at: https://wallet.pirl.io/.  
 - Whichever method you choose to create your wallet, always make sure you save your UTC file and password!
 - Warning: UTC Passwords cannot be recovered, make sure you remember it or write it down!

* **20,001 Pirl available in your wallet for Premium MN**

 - There’s no getting around it, you will need to somehow get twenty thousand PIRL into a wallet.
 - And 1 or 0,5 for gas to interact with the contract.
 - You can mine Pirl by using one of the official pools available here: https://pirl.io/en/pools/.
 - You can also buy Pirl on one of the Pirl exchanges. I recommend [https://www.stex.com](https://app.stex.com/de/trade/pair/BTC/PIRL/1D) as a safe and reliable exchange.

## Poseidon Wallet Identity Verification

- Navigate to https://poseidon.pirl.io/ and login -> Navigate to Poseidon Wallet https://poseidon.pirl.io/dashboard/accounting/wallet/ and copy your unique Poseidon Wallet Address.

- Open your Nautilus or Web Wallet (whichever you choose to use and keep the stake in) and send 0.5 PIRL to the Poseidon Wallet Address you copied in the previous step.

- Once you sent the verification transaction, navigate to https://explorer.pirl.network/ and paste your wallet address in the search bar. This search will display your wallet and its relevant transactions. -> Locate the last transaction of 0.5 PIRL from your wallet to your poseidon wallet.

- The first row of the transaction block displays the transaction hash. You will need this transaction hash later during the setup in order to verify the link between your masternode and your poseidon wallet.

![](https://i.imgur.com/tAWr8Ua.png)

> **Note:** Do not send anymore then 1 or 0.5 Pirl to this address for verfication, this is NOT the address you will send the 20k pirls to. That comes later.

If you are using nautilus wallet you can click once on the last sent transaction and you see the Transaction Hash(Later asked in Masternode TX Hash field):

{{< imagesurlsheaders "cloud/txnautilus.png" >}}

## Nautilus Contract Execution

- **Open Nautilus** and navigate to the **Contract** tab located at the top right corner.

![](https://cdn-images-1.medium.com/max/1600/0*OW_7W9P_u0k7ZdmZ.png)

- Once there, click on the **Watch Contract** button.

![](https://cdn-images-1.medium.com/max/1600/0*wZbZlfAdjrUuhr53.png)

**In this form you need to fill in:**

- **Premium MN:** For **Contract Address** fill in `0x256b2b26Fe8eCAd201103946F8C603b401cE16EC`. The **Contract Name** contract name for this is premium even though it can be anything you’d like.

- And lastly, the **JSON Interface field** needs to be populated with:

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

Monitor the status of your masternode by checking the Poseidon Masternode Details page by clicking on the 🔍.
A functioning node should appear as follows:


{{< imagesurlsheaders "cloud/detailsmn.png" >}}

---
Author(s):

The Pirl Team

Contributor(s):

@Dptelecom
