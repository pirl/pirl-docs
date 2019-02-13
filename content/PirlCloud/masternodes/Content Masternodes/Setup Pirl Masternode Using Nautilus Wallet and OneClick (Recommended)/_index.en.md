---
title: Setup Content Masternode
weight: 1
pre: "<b>1. </b>"
chapter: true
---
![](/images_headers/Masternodes.png)



- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Poseidon Wallet Identity Verification](#poseidon-wallet-identity-verification)
- [Nautilus Contract Execution](#nautilus-contract-execution)
- [Create/Launch CentOS Linux server](#create-launch-centos-linux-server)
- [Create Masternode in Poseidon](#create-masternode-in-poseidon)
- [One-Click Masternode Setup](#one-click-masternode-setup)
- [Monitoring](#monitoring)




## Overview

Running a PIRL masternode requires the use of a Virtual 
Private Server (VPS) with a static public IP address directly assigned to an interface.  
*NAT (address translation) is not supported.*
And only have pirl running on the server, no other nodes or whatever cause it will cause conflict!!


Once you have the funds in place, 
you send a small 1 PIRL transaction to your Poseidon wallet (your account will come with a wallet) to prove that you control the Nautilus wallet with the 10K PIRL capital for Content MN.  
You use the txid from the 1 PIRL transaction as part of the masternode setup, along with your Nautilus address. 
When the masternode is added, 
you go back to your Nautilus wallet and add the masternode contract address in the “contracts” tab.  
With the masternode contract address in place, 
you execute the node registration function.  
At this point  you can utilize the Poseidon one-click functionality which will automatically setup your server and keep it updated.

This guide uses the one-click-masternode setup feature. 
This Poseidon feature automatically configures your CentOS 7 linux server to be a Pirl Masternode. 
Updates will be applied automatically. 
All you have to do is monitor your server to ensure it stays operational. 
This is as simple as rebooting the server, should it go offline. 


## Prerequisites

* **A VPS with minimum 4GB Total OS RAM minimum (more is recommended), enough storage to run the masternode (Minimum 20GB, Recommended 60GB+), and a static public IP address directly assigned to an interface.  NAT (address translation) is not supported.**
 - The official MINIMUM requirements are: 4GB RAM, 20GB space, 3TB transfer, public IPv4 IP. Once you order your VPS, you will receive its root credentials. The easiest path forward is to only use this VPS for your Pirl Masternode and give Poseidon your root credentials so it can manage and update your VPS.
* **A Poseidon account on [https://poseidon.pirl.io](https://poseidon.pirl.io)**
 - Navigate over to https://poseidon.pirl.io and register for an account.  Keep in mind that you will be logging in with your username and not email.
* **Nautilus wallet**
 - Nautilus is the official desktop wallet for Pirl.  You will need it in order to add and execute “Register Node” from the smart contract needed to run the Pirl masternode.  You can use the desktop wallet to create your Pirl wallet [Downloads Nautilus]({{< ref "/Downloads" >}}) or you can use the web wallet at: https://wallet.pirl.io/.  
 - Whichever method you choose to create your wallet, always make sure you save your UTC file, 
 - the password needed to decrypt the UTC file as well as your private key.  
 - You can use your Nautilus created UTC file and password to extract your private key.  
 - You can use your private key instead of the UTC file + Password to access your wallet and withdraw your funds in case of an emergency.
* **10,001 Pirl available in your wallet for Content MN**
 - There’s no getting around it, you will need to somehow get ten thousand PIRL into a wallet.
 - And 1 or 0,5 for gas to interact with the contract.
 - You can mine Pirl by using one of the official pools available here: https://pirl.io/en/pools/. 
 - You can also buy Pirl on one of the Pirl exchanges. I recommend https://www.stex.com as a safe and reliable exchange. 


## Poseidon Wallet Identity Verification

The first step in the masternode setup process is to send a transaction from your Nautilus wallet (you can also use the web wallet here if needed) to your Poseidon wallet located here: https://poseidon.pirl.io/dashboard/accounting/wallet/.  
This is just like sending Pirl to any other wallet, except in this case it’s your unique Poseidon wallet.  
What this does is it proves to Poseidon that you control your Nautilus wallet.
Do not send anymore then 1 or .5 pirl to this address for verfication, this is not the address you will send the 10k pirls to. that comes later.

Navigate over to https://poseidon.pirl.io/ and paste your Nautilus wallet address at the top.  
This will show all transactions in and out of your Nautilus wallet.  
The latest outgoing transaction will show that it’s going into the address of your Poseidon wallet.  
To the very left of the page, the txid (i.e. transaction hash) will be displayed.  
Or In the nautilus wallet you click once on the sent transaction and you see this Tx-id:
Take and safe this txid and copy it because you’ll need it later.

**VERY IMPORTANT: There are 2 hashes for every transaction.  
There is the transaction hash (txid) and the block hash.  
You need to use the transaction hash (txid) for the masternode setup process to work.  
There’s a very easy way to know which one is the txid.  
The txid is on the left side of the general transaction list of your wallet.  
Once you click on the txid itself, you will see the block hash displayed.  
o not use the block hash.  
Use the txid on the left most side of your wallet transaction list on Poseidon**

![](https://cdn-images-1.medium.com/max/1600/0*1LTQiVdFomhRei6u.png)
![](https://cdn-images-1.medium.com/max/1600/0*bVaXgKomLeN0mEYQ.png)


In the nautilus wallet you click once on the sent transaction and you see this Tx-id:

![](/PirlCloud/images/txnautilus.png)


## Nautilus Contract Execution

Now that we have the hardest part out of the way, let’s move on Nautilus and adding the Pirl Masternode contract.

**Open Nautilus** and navigate to the **Contract** tab located at the top right corner.

![](https://cdn-images-1.medium.com/max/1600/0*OW_7W9P_u0k7ZdmZ.png)

Once there, click on the **Watch Contract** button.

![](https://cdn-images-1.medium.com/max/1600/0*wZbZlfAdjrUuhr53.png)


There are two contracts 1 for each type of node,
the JSON is for all the Masternodes the same


**Content MN:** For **Contract Address** fill in `0x6c042141C302C354509d2bff30EEFDEF24dE1047`. 
The **Contract Name** contract name for this is content
even though it can be anything you’d like.   
And lastly, the **JSON Interface field** needs to be populated with:


```
[{"constant":false,"inputs":[],"name":"nodeRegistration","outputs":[{"name":"paid","type":"bool"}],"payable":true,"stateMutability":"payable","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getNodeAddress","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"","type":"address"}],"name":"moderators","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"","type":"address"}],"name":"nodes","outputs":[{"name":"pirlAddress","type":"address"},{"name":"nodeStake","type":"uint256"},{"name":"nodeHash","type":"bytes20"},{"name":"stakeLocked","type":"bool"},{"name":"nodeEnabled","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"disableNodeRegistration","outputs":[{"name":"disabled","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"nodeCost","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getStakeLockedStatus","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"nodeCount","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[{"name":"_admin","type":"address"}],"name":"setAdmin","outputs":[{"name":"set","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"owner","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"enableNode","outputs":[{"name":"enabled","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"nodeRegistrationEnabled","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"disableNode","outputs":[{"name":"disabled","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":false,"inputs":[],"name":"withdrawStake","outputs":[{"name":"withdrawn","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[{"name":"","type":"uint256"}],"name":"nodeAddresses","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getNodeEnabledStatus","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getNodeStake","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"enableNodeRegistration","outputs":[{"name":"enabled","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getNodeHash","outputs":[{"name":"","type":"bytes20"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"nodeFee","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"admin","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"inputs":[],"payable":false,"stateMutability":"nonpayable","type":"constructor"},{"payable":true,"stateMutability":"payable","type":"fallback"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_nodeRegistered","type":"bool"},{"indexed":false,"name":"_dateRegistered","type":"uint256"}],"name":"MasterNodeRegistered","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_nodeDisabled","type":"bool"},{"indexed":false,"name":"_dateDisabled","type":"uint256"}],"name":"MasterNodeDisabled","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_nodeEnabled","type":"bool"},{"indexed":false,"name":"_dateEnabled","type":"uint256"}],"name":"MasterNodeEnabled","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_nodePaid","type":"bool"},{"indexed":false,"name":"_datePaid","type":"uint256"}],"name":"MasterNodeRewarded","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_stakeWithdrawn","type":"bool"},{"indexed":false,"name":"_dateWithdrawn","type":"uint256"}],"name":"StakeWithdrawn","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_invoker","type":"address"},{"indexed":false,"name":"_dateEnabled","type":"uint256"},{"indexed":true,"name":"_registrationEnabled","type":"bool"}],"name":"MasterNodeRegistrationEnabled","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_invoker","type":"address"},{"indexed":false,"name":"_dateDisabled","type":"uint256"},{"indexed":true,"name":"_registrationDisabled","type":"bool"}],"name":"MasterNodeRegistrationDisabled","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_invoker","type":"address"},{"indexed":true,"name":"_admin","type":"address"},{"indexed":true,"name":"_adminSet","type":"bool"}],"name":"SetAdmin","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_invoker","type":"address"},{"indexed":true,"name":"_newOwner","type":"address"},{"indexed":true,"name":"_ownerChanged","type":"bool"}],"name":"TransferOwnership","type":"event"}]
```


Select the newly address Masternode contract and you will see available functions for it as a dropdown menu on the right side under the **Write to Contract** heading. 
Under available functions select **Node Registration** and select the wallet containing your 10,000 Pirl for Content MN. 
Underneath that, fill in  **10,000 Pirl** for Content MN to send the stake to the contract.

![](/PirlCloud/images/10k.png)


Once you hit **execute**, fill in your **UTC file password** and make sure you’re providing **at least 121,000 gas** for the transaction.

This is a good time to get some coffee or tea and let everything sync.  3-5 minutes should do the trick.

## Create/Launch CentOS Linux server

Verify that the server meets the appropriate specifications as noted in the [Pirl Masternode Setup Tutorial](https://pirl.io/blog/1-pirl-masternode-setup-tutorial)

The server must run the CentOS 7 Linux distribution if you plan to use the **One-Click Masternode Setup**.

Record of the static public IP address of the server as well as the root password. 
We do recommend logging into that server once to ensure the `root` credentials work. 
It is not necessary to take any other actions on the server after that. 
In fact, it's preferred that you don't make any other adjustments, at all.




## Create Masternode in Poseidon

Login to Poseidon and navigate to the page which adds a masternode located here:   
https://poseidon.pirl.io/dashboard/masternodes/  
and hit the:  

![](/PirlCloud/images/redcrossadd.jpg)


then you get this nice popup screen:

![](/PirlCloud/images/Create_content_Masternode_Record_in_Poseidon.png)


The Name can be anything you’d like.  
The Masternode Wallet id is the address of your Nautilus wallet, the one which contains 10,000 Pirl at present.  
And, remember, 
the Tx hash validation field needs the txid (not block hash, see above!) of the transaction you send to your Poseidon wallet.

**On the bottom of the screenshot above, you will have to select that the MN is Content (10K stake)**

Hit **Save changes** and then you will see the next screen.

![](/PirlCloud/images/one_click_setup.PNG)



## One-Click Masternode Setup

Ensure that you know the public static IP address and `root` credentials before proceeding.


![](/PirlCloud/images/one_click_setup.PNG)


we go and complete all fields.
ssh default is port: 22
Hit **Save changes** and then you will see the next screen.
content/PirlCloud/images/Done.PNG

![](/PirlCloud/images/Done.PNG)

After returning to the **My Masternodes** screen, observe that the masternode's **Managed by Poseidon** field is set to `True`

![](/PirlCloud/images/managed.jpg)

Please allow 30 minutes for the process to complete. You may click the **details** button to monitor the status.

Watch the masternode process synchronize with the blockchain:
```
journalctl -f
```

Once messages like the following are displayed, your masternode is now synchronized and contributing to the network.


![](/PirlCloud/images/vps.jpg)




## Monitoring

We don't encourage active access on the server.  If, however, you wish to check the status, log into your server and issue the following command:
```
journalctl -f
```

your masternode is contributing to the network if it looks like this:.


![](/PirlCloud/images/vps.jpg)


Monitor the status of your masternode by checking the Poseidon Masternode Details page by clicking on the 🔍.   
A functioning node should appear as follows:

![](/PirlCloud/images/detailsmn.png)



---
Author(s):


The Pirl Team


Contributor(s):


@Dptelecom