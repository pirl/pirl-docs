---
title: Pirl Masternode token change how to...
weight: 5
disableToc: true
---

## Overview

This guide will help you change the masternode token of your masternode. The masternode token and the user token comprise the 2 tokens each masternode service on a VPS. You can check your [user token on Poseidon](https://poseidon.pirl.io/accounts/settings/) by going clicking **Profile > Settings**.

**The one-click masternode setup users will usually not have to do this as the process can be initiated remotely by Poseidon**


## How to Change the Token

**Open Poseidon** [Poseidon](https://poseidon.pirl.io/accounts/masternodes-list-private/)

The Masternode TOKEN is found here:

On the left menu, click on **Masternodes > My masternodes**.
You will see next to the masternode you created earlier, the masternode token under **MN token**.

![](content/masternodes/Pirl Masternode token change how to/images/Mn_token.jpg)


**Log in to your VPS**

Update the file with ypour Masternode token in it.
Depending on how it was setup, it will be in one of the following files:

`/etc/pirlnode.env`

`/etc/pirl.env`

`/etc/pirlnode-env`

`/etc/systemd/system/pirlnode.service`

```
cat /etc/pirlnode-env
```

You need to edit the file, with a file editor like: *vi, vim, joe, nano, pico*

```
nano:

nano /etc/pirlnode-env

joe:

joe /etc/pirlnode-env
```

```
MASTERNODE="11111111-1111-1111-1111-111111111111"
TOKEN="1111111111111111111111111111111111111111"
```

**(Note: You need to change the MASTERNODE token above. The bottom one is your user token and does not need to be changed.)**

oO like this using `vi`:

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

and restart the service:
```
systemctl restart pirlnode
```
or this one:
```
systemctl restart pirl
```


---
Author(s):
_dptelecom.

Contributor(s):
Phatblinkie thanks for your info.

[PrimateCrypto](https://twitter.com/PrimateCrypto) thanks for your info.
