---
title: Staking Pirl Masternode From Hardware Wallet Using Web Wallet
weight: 4
pre: "<b>4. </b>"
chapter: true
---

## Overview

Running a PIRL masternode requires the use of a Virtual Private Server (VPS) with a static public IP address directly assigned to an interface.

This guide uses the one-click-masternode setup feature. This is an optional feature for those that wish to have a more hands-off experience with the setup of their masternode. This Poseidon feature automatically configures your CentOS7 linux server to be a Pirl Masternode. Updates will be applied automatically. All you have to do is monitor your server to ensure it stays operational. This is as simple as rebooting the server, should it go offline. Manual installation instructions are also provided for those that want a bit more control of the system.

## Prerequisites

* A VPS with minimum **4GB Total OS RAM minimum** (more is recommended), enough storage to run the masternode (**Minimum 20GB**, Recommended 60GB+), and a **Public IP** assigned at the network interface
* A JSON wallet address or a hardware wallet compatible with [https://wallet.pirl.io](https://wallet.pirl.io).  You may import your JSON wallet from Nautilus if you so choose.
* A Poseidon account on [https://poseidon.pirl.io](https://poseidon.pirl.io)
* 20001 Pirl available in your wallet for a **premium masternode**, or 10001 Pirl for a **content node**.

## Poseidon Wallet Identity Verification

Go to the web wallet and choose the **Send Ether & Tokens** tab.

![](https://cdn-images-1.medium.com/max/1000/1*rBNbzQmdBafw5IzeIb2zuA.png)

Send a small amount of Pirl from your wallet account that holds 20001 (or 10001) Pirl to your Poseidon address. My screenshots show that I sent 0.1 Pirl, although officially, 0.5 Pirl is recommended. Any small amount should do.  Save the Tx hash - you will need this later.

CAUTION: Users have confused the Tx hash with the block hash in the past.  The block hash will not work - you must get the transaction hash!

![](https://cdn-images-1.medium.com/max/1000/1*dk8HBn5i2o3R9Edppfqkgg.png)

## Masternode Registration

Go to the web wallet and choose the **Contracts** tab.

![](https://cdn-images-1.medium.com/max/1000/1*WgStoJFt0ngeYpD8JxYFRQ.png)

From the **Select Existing Contract** drop-down box, select either **Premium Masternode Administration** or **Content Node Administration**

![](https://cdn-images-1.medium.com/max/1000/1*FfUJJvGS4hNUpymZdLUz9Q.png)

You should see the ABI / JSON Interface populate.

![](https://cdn-images-1.medium.com/max/1000/1*ZFXljjcYPyXKwpMwlzMl9A.png)

Click the **Access** button, then **Read / Write Contract** will come up.

![](https://cdn-images-1.medium.com/max/1000/1*07Q-npFDNNL6AfOfNx32KQ.png)

Select **nodeRegistration** from the **Select a function** drop-down box.

![](https://cdn-images-1.medium.com/max/1000/1*i5G1VIRI_tptLhJkWoGuZA.png)

Choose the method in which you will access your wallet.

![](https://cdn-images-1.medium.com/max/1000/1*pl1f1XDSPtmH-h0LLGdotg.png)

Select the wallet address that contains your funds, and click the **Unlock your Wallet** button.

![](https://cdn-images-1.medium.com/max/800/1*gzzNzHTgMgdWI4m4goVgkA.png)

A message should quickly flash on the bottom of the screen, saying **Wallet successfully decrypted**.  Don't worry if you miss the message - it's just a confirmation, and it doesn't show you any new information.

To send your Pirl stake to the masternode smart contract, click the **WRITE** button.

![](https://cdn-images-1.medium.com/max/1000/1*ZccjsKPBWAePARfBuM0aqg.png)

The **execute function on contract** dialog box will appear.  Fill in your amount (20000 for premium masternodes, 10000 for content nodes) and make sure the Gas Limit is high enough, then click **Generate Transaction**

![](https://cdn-images-1.medium.com/max/800/1*kd8tInNtodfN0son6SYjOA.png)

Confirm the transaction on your hardware wallet

![](https://cdn-images-1.medium.com/max/800/1*CPtbglUs8sRJ4r9rtncuOA.jpeg)

Click **Yes, I am sure! Make transaction.**

![](https://cdn-images-1.medium.com/max/800/1*efwUMKLanP6l9gysgcLtJw.png)

Notice the transaction flash on the bottom.  Don't worry if you miss it - you don't need to capture any of this information

![](https://cdn-images-1.medium.com/max/1000/1*EJ7YIcrqJKEhXBbWJiNNHw.png)

## Add Masternode Entry To Poseidon

Go back to Poseidon and choose **Masternodes** from the left menu, then **Create masternode**.

![](https://cdn-images-1.medium.com/max/800/0*AZXW-yLdgOdqaxSn.png)

Name the masternode whatever you like.  The wallet ID must match the wallet address you used for your funds.

Enter the saved Tx hash from earlier in the box labeled, **Tx hash validation**.

You will now see the newly created masternode entry under **My Masternodes**.

Before moving forward, you must wait for Poseidon to issue a masternode token. If you are using the **One-Click Install** you don't have to wait.

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

The instructions are intended for Redhat or CentOS based VPS but should work on most major Linux distributions. You may have the need to adjust the firewall instructions to match the software software running on your VPS.

Login as root and update the system, then install dependencies:
```
yum update
sudo yum install wget systemd -y
```

Set up firewall rules:
```
firewall-cmd --zone=public --add-port=22/tcp --permanent
firewall-cmd --zone=public --add-port=4001/tcp --permanent
firewall-cmd --zone=public --add-port=6588/tcp --permanent
firewall-cmd --zone=public --add-port=6589/tcp --permanent
firewall-cmd --zone=public --add-port=30303/tcp --permanent
firewall-cmd --zone=public --add-port=30303/udp --permanent
firewall-cmd  --reload
```

Create a `pirl` user and add it to the `systemd-journal` group:
```
adduser pirl && passwd pirl
usermod -aG systemd-journal pirl
```

Download the premium masternode binaries:
```
wget https://git.pirl.io/community/pirl/uploads/8f3823838355d18b5d6d9b16129c2499/pirl-linux-amd64-v5-masternode-premium-hulk
wget https://git.pirl.io/community/pirl/uploads/f991222e04b2525cfb4a94a078f7247b/marlin-v5-masternode-premium-hulk
```

...or the content node binaries:
```
wget https://git.pirl.io/community/pirl/uploads/9f6b22ff763e01353648202bb3718e74/pirl-linux-amd64-v5-masternode-content-hulk
wget https://git.pirl.io/community/pirl/uploads/7b44acaa183a620bd1e57c1663ee9b72/marlin-v5-masternode-content-hulk
```



Move the main binary to `/usr/bin/pirl`:

For premium masternodes:
```
mv pirl-linux-amd64-v5-masternode-premium-hulk /usr/bin/pirl
```

For content nodes:
```
mv pirl-linux-amd64-v5-masternode-content-hulk /usr/bin/pirl
```


Move the marlin binary to `/usr/bin/marlin`:

For premium masternodes:
```
mv marlin-v5-masternode-premium-hulk /usr/bin/marlin
```

For content nodes:
```
mv marlin-v5-masternode-content-hulk /usr/bin/marlin
```


Create a system service file for the pirl service:
```
vi /lib/systemd/system/pirl.service
```

Press the `i` button to enter insertion mode, then add the following.  Be sure to add your own MASTERNODE and user TOKEN to the Environment under the `[Service]` section:
```
[Unit]
Description=Pirl Node

[Service]
; location of the file with the exported variables
;EnvironmentFile=/etc/pirlnode-env
Environment=MASTERNODE=YoUR MaSTErNodE ToKEn GoES HeRE
Environment=TOKEN=YoUR UsER ToKEn GoES HeRE
Type=simple
ExecStart=/usr/bin/pirl --ws --wsorigins=* --wsaddr=0.0.0.0 --rpc --rpcaddr=0.0.0.0 --rpccorsdomain="*"
Restart=always
ExecStartPre=/bin/sleep 5
RestartSec=30s
RemainAfterExit=no


[Install]
WantedBy=multi-user.target
```


Create a system service file for the marlin service:
```
vi /lib/systemd/system/marlin.service
```

Press the `i` button to enter insertion mode, then add the following.  Be sure to add your own MASTERNODE and user TOKEN to the Environment under the `[Service]` section:
```
[Unit]
Description=Marlin Master Node

[Service]
; location of the file with the exported variables
Environment=MASTERNODE=YoUR MaSTErNodE ToKEn GoES HeRE
Environment=TOKEN=YoUR UsER ToKEn GoES HeRE
Type=simple
ExecStart=/usr/bin/marlin daemon
Restart=always
ExecStartPre=/bin/sleep 5
RestartSec=30s
User=root

[Install]
WantedBy=default.target
```

Enable and start the pirlnode service:
```
systemctl daemon-reload
systemctl enable pirl
systemctl restart pirl
```



Enable and start the pirlmarlin service:
```
systemctl enable marlin
/usr/bin/marlin init
systemctl start marlin
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
_[PrimateCrypto](https://twitter.com/PrimateCrypto)_, _[masterdubs](https://twitter.com/mast3rdubs)_
