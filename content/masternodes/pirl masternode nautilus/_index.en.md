---
title: Configuring Pirl Masternode Using Nautilus Wallet
weight: 5
disableToc: true
---

## Overview

Running a PIRL masternode requires the use of a Virtual Private Server (VPS) with a static public IP address directly assigned to an interface.

Once you have the funds in place, you send a small 1 PIRL transaction to your Poseidon wallet (your account will come with a wallet) to prove that you control the Nautilus wallet with the 20K PIRL capital.  You use the txid from the 1PIRL transaction as part of the masternode setup, along with your Nautilus address. When the masternode is added, you go back to your Nautilus wallet and add the masternode contract address in the “contracts” tab.  With the masternode contract address in place, you execute the node registration function.  At this point you can either manually install the PIRL masternode binary and configure the masternode and firewall on your dedicated server or VPS or you can utilize the Poseidon 1 click functionality which will automatically setup your server and keep it updated.

This guide uses the one-click-masternode setup feature. This is an optional feature for those that wish to have a more hands-off experience with the setup of their masternode. This Poseidon feature automatically configures your CentOS7 linux server to be a Pirl Masternode. Updates will be applied automatically. All you have to do is monitor your server to ensure it stays operational. This is as simple as rebooting the server, should it go offline. Manual installation instructions are also provided for those that want a bit more control of the system.

## Prerequisites

* **A VPS with minimum 4GB RAM and enough storage to run the masternode (minimum 20GB, recommended 60GB)**
 - The official requirements are: 4GB RAM, 20GB space, 3TB transfer, public IPv4 IP. Once you order your VPS, you will receive its root credentials. The easiest path forward is to only use this VPS for your Pirl Masternode and give Poseidon your root credentials so it can manage and update your VPS.
* **A Poseidon account on [https://poseidon.pirl.io](https://poseidon.pirl.io)**
 - Navigate over to https://poseidon.pirl.io and register for an account.  Keep in mind that you will be logging in with your username and not email.
* **Nautilus wallet**
 - Nautilus is the official desktop wallet for Pirl.  You will need it in order to add and execute “Register Node” from the smart contract needed to run the Pirl masternode.  You can use the desktop wallet to create your Pirl wallet or you can use the web wallet at: https://wallet.pirl.io/.  Whichever method you choose to create your wallet, always make sure you save your UTC file, the password needed to decrypt the UTC file as well as your private key.  You can use your Nautilus created UTC file and password to extract your private key.  You can use your private key instead of the UTC file + Password to access your wallet and withdraw your funds in case of an emergency.
* **20001 Pirl available in your wallet.**
 - There’s no getting around it, you will need to somehow get twenty thousand PIRL into a wallet. You can mine Pirl by using one of the official pools available here: https://pirl.io/en/pools/. You can also buy Pirl on one of the Pirl exchanges. I recommend https://www.cryptopia.co.nz/ as a safe and reliable exchange. There is also the “OTC” (over the counter)

## Poseidon Wallet Identity Verification

The first step in the masternode setup process is to send a transaction from your Nautilus wallet (you can also use the web wallet here if needed) to your Poseidon wallet located here: https://poseidon.pirl.io/accounts/wallet/.  This is just like sending Pirl to any other wallet, except in this case it’s your unique Poseidon wallet.  What this does is it proves to Poseidon that you control your Nautilus wallet.

Navigate over to https://poseidon.pirl.io/ and paste your Nautilus wallet address at the top.  This will show all transactions in and out of your Nautilus wallet.  The latest outgoing transaction will show that it’s going into the address of your Poseidon wallet.  To the very left of the page, the txid (i.e. transaction hash) will be displayed.  Take and safe this txid and copy it because you’ll need it later.

**VERY IMPORTANT: There are 2 hashes for every transaction.  There is the transaction hash (txid) and the block hash.  You need to use the transaction hash (txid) for the masternode setup process to work.  There’s a very easy way to know which one is the txid.  The txid is the one you can click on as a link.  However, once you click on the txid, you will see the block hash displayed.  Do not use the block hash.**

![](https://cdn-images-1.medium.com/max/1600/0*1LTQiVdFomhRei6u.png)
![](https://cdn-images-1.medium.com/max/1600/0*bVaXgKomLeN0mEYQ.png)

## Create Masternode Record in Poseidon

Login to Poseidon and navigate to the page which adds a masternode located here: https://poseidon.pirl.io/accounts/create-masternodes/

![](https://cdn-images-1.medium.com/max/1600/0*LXUIRuqHwrNd4JBw.png)

The Name can be anything you’d like.  The Wallet id is the address of your Nautilus wallet, the one which contains 20,000 Pirl at present.  And, remember, the Tx hash validation field needs the txid (not block hash, see above!) of the transaction you send to your Poseidon wallet.

## Nautilus Contract Execution

Now that we have the hardest part out of the way, let’s move on Nautilus and adding the Pirl Masternode contract.

**Open Nautilus** and navigate to the **Contract** tab located at the top right corner.

![](https://cdn-images-1.medium.com/max/1600/0*OW_7W9P_u0k7ZdmZ.png)

Once there, click on the **Watch Contract** button.

![](https://cdn-images-1.medium.com/max/1600/0*wZbZlfAdjrUuhr53.png)

For **Contract Address** fill in `0x256b2b26Fe8eCAd201103946F8C603b401cE16EC`. The **Contract Name** can be anything you’d like.  And lastly, the **JSON Interface field** needs to be populated with:

```
[{"constant":false,"inputs":[],"name":"nodeRegistration","outputs":[{"name":"paid","type":"bool"}],"payable":true,"stateMutability":"payable","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getNodeAddress","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"","type":"address"}],"name":"moderators","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"","type":"address"}],"name":"nodes","outputs":[{"name":"pirlAddress","type":"address"},{"name":"nodeStake","type":"uint256"},{"name":"nodeHash","type":"bytes20"},{"name":"stakeLocked","type":"bool"},{"name":"nodeEnabled","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"disableNodeRegistration","outputs":[{"name":"disabled","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"nodeCost","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getStakeLockedStatus","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"nodeCount","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[{"name":"_admin","type":"address"}],"name":"setAdmin","outputs":[{"name":"set","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"owner","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"enableNode","outputs":[{"name":"enabled","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"nodeRegistrationEnabled","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"disableNode","outputs":[{"name":"disabled","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":false,"inputs":[],"name":"withdrawStake","outputs":[{"name":"withdrawn","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[{"name":"","type":"uint256"}],"name":"nodeAddresses","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getNodeEnabledStatus","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getNodeStake","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"enableNodeRegistration","outputs":[{"name":"enabled","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getNodeHash","outputs":[{"name":"","type":"bytes20"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"nodeFee","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"admin","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"inputs":[],"payable":false,"stateMutability":"nonpayable","type":"constructor"},{"payable":true,"stateMutability":"payable","type":"fallback"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_nodeRegistered","type":"bool"},{"indexed":false,"name":"_dateRegistered","type":"uint256"}],"name":"MasterNodeRegistered","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_nodeDisabled","type":"bool"},{"indexed":false,"name":"_dateDisabled","type":"uint256"}],"name":"MasterNodeDisabled","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_nodeEnabled","type":"bool"},{"indexed":false,"name":"_dateEnabled","type":"uint256"}],"name":"MasterNodeEnabled","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_nodePaid","type":"bool"},{"indexed":false,"name":"_datePaid","type":"uint256"}],"name":"MasterNodeRewarded","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_stakeWithdrawn","type":"bool"},{"indexed":false,"name":"_dateWithdrawn","type":"uint256"}],"name":"StakeWithdrawn","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_invoker","type":"address"},{"indexed":false,"name":"_dateEnabled","type":"uint256"},{"indexed":true,"name":"_registrationEnabled","type":"bool"}],"name":"MasterNodeRegistrationEnabled","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_invoker","type":"address"},{"indexed":false,"name":"_dateDisabled","type":"uint256"},{"indexed":true,"name":"_registrationDisabled","type":"bool"}],"name":"MasterNodeRegistrationDisabled","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_invoker","type":"address"},{"indexed":true,"name":"_admin","type":"address"},{"indexed":true,"name":"_adminSet","type":"bool"}],"name":"SetAdmin","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_invoker","type":"address"},{"indexed":true,"name":"_newOwner","type":"address"},{"indexed":true,"name":"_ownerChanged","type":"bool"}],"name":"TransferOwnership","type":"event"}]
```

Select the newly address Masternode contract and you will see available functions for it as a dropdown menu on the right side under the **Write to Contract** heading. Under available functions select **Node Registration** and select the wallet containing your 20,000 Pirl. Underneath that, fill in **20,000 Pirl** to send

![](https://cdn-images-1.medium.com/max/1600/0*eiHNFfmkEcgv5Szo.png)

Once you hit **execute**, fill in your **UTC file password** and make sure you’re providing **at least 121,000 gas** for the transaction.

This is a good time to get some coffee or tea and let everything sync.  3-5 minutes should do the trick.

## Create/Launch CentOS Linux server

Verify that the server meets the appropriate specifications as noted in the [Pirl Masternode Setup Tutorial](https://pirl.io/blog/1-pirl-masternode-setup-tutorial)

The server must run the CentOS 7 Linux distribution if you plan to use the **One-Click Masternode Setup**.

Record of the static public IP address of the server as well as the root password. We do recommend logging into that server once to ensure the `root` credentials work. It is not necessary to take any other actions on the server after that. In fact, it's preferred that you don't make any other adjustments, at all.

Now proceed to either the **One-Click Masternode Setup** or the **Manual Masternode Setup**. (One-Click is recommended)

## One-Click Masternode Setup

Ensure that you know the public static IP address and `root` credentials before proceeding.

Login to Poseidon. On the left menu, choose Masternodes -> My Masternodes. You should see the following:

![](https://cdn-images-1.medium.com/max/1000/1*N2NyFBXJgHqjaPA4nUw8qA.png)

Click the **One-Click MN Setup** button and complete all fields.

![](https://cdn-images-1.medium.com/max/1000/1*crfDegFUCQo-tCHczi6GHQ.png)

After returning to the **My Masternodes** screen, observe that the masternode's **Managed by Poseidon** field is set to `True`

![](https://cdn-images-1.medium.com/max/1000/1*wef5d-8ZNtHlQDwX5lAemw.png)

Please allow 30 minutes for the process to complete. You may click the **details** button to monitor the status.

-or-

If you prefer a manual setup rather than using the **One-Click MN Setup** Guide, follow the next steps.

## Manual Masternode Setup

Login as root and update the system, then install dependencies:
```
yum update
sudo yum install wget systemd -y
```

Set up firewall rules:
```
firewall-cmd --zone=public --add-port=22/tcp --permanent
firewall-cmd --zone=public --add-port=30303/tcp --permanent
firewall-cmd --zone=public --add-port=30303/udp --permanent
firewall-cmd  --reload
```

Create a `pirl` user and add it to the `wheel` group:
```
adduser pirl && passwd pirl
usermod -aG wheel pirl
```

Download the masternode binary:
```
wget http://release.pirl.io/downloads/masternode/linux/pirl-linux-amd64
```

Mark it executable, and change its owner to `pirl:pirl`:
```
chmod 755 pirl-linux-amd64
chown pirl:pirl pirl-linux-amd64
```

Move the binary to `/usr/sbin/pirl-geth`:
```
mv pirl-linux-amd64 /usr/sbin/pirl-geth
```

Create a system service file:
```
vi /etc/systemd/system/pirlnode.service
```

Press the `i` button to enter insertion mode, then add the following.  Be sure to add your own MASTERNODE and user TOKEN to the Environment under the `[Service]` section:
```
[Unit]
Description=Pirl Client -- masternode service
After=network.target

[Service]
Environment=MASTERNODE=YoUR MaSTErNodE ToKEn GoES HeRE
Environment=TOKEN=YoUR UsER ToKEn GoES HeRE

User=pirl
Group=pirl
Type=simple
Restart=always
RestartSec=30s
ExecStart=/usr/sbin/pirl-geth

[Install]
WantedBy=default.target
```

Enable and start the new service:
```
systemctl enable pirlnode
systemctl restart pirlnode
```

Watch the masternode process synchronize with the blockchain:
```
journalctl -f
```

Once messages like the following are displayed, your masternode is now synchronized and contributing to the network.
```
########  masternode sending proof of activity for block 2051449 please check poseidon.pirl.io for details  #########
```

## Monitoring

We don't encourage active access on the server.  If, however, you wish to check the status, log into your server and issue the following command:
```
journalctl -f
```

Monitor the status of your masternode by checking the Poseidon Masternode Details page. A functioning node should appear as follows, although the version may be different than what is shown in the screen shot below.

![](https://cdn-images-1.medium.com/max/800/1*PFDEiPPUfl1Q2qzc0YWFlQ.png)

---
Author(s):
_[Michael Ira Krufky](https://github.com/mkrufky) is a Senior Systems Engineer at Vimeo in New York.  He has been an active open source developer for years, contributing to projects such as [nodejs/nan](https://github.com/nodejs/nan), `video4linux`, `linux-dvb`, `linux-kernel`, `libdvbpsi` and his own digital video capture and streaming middleware solution, [dvbtee](https://github.com/mkrufky/libdvbtee)._

Contributor(s):
_[PrimateCrypto](https://twitter.com/PrimateCrypto)_
