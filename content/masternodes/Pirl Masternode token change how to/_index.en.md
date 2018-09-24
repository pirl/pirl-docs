---
title: Pirl Masternode token change how to...
weight: 5
disableToc: true
---

## Overview

This guide will help you change the token on the Masternode
**the one-click-masternode setup users will not have to do this!**


## How to change the token.

**Open Poseidon** [Poseidon](https://poseidon.pirl.io/accounts/masternodes-list-private/)

The Masternode TOKEN is found here:

On the left menu, click on Masternodes -> My masternodes. 
You will see next to the masternode you created earlier, the masternode token under "MN token".

![](https://git.pirl.io/community/pirl-docs/blob/master/content/masternodes/Pirl%20Masternode%20token%20change%20how%20to/images/Mn_token.jpg)



**log in to your vps**

update the file with ypour Masternode token in it 
depending on how it was setup its in one of this files:

/etc/pirlnode.env

/etc/pirl.env

/etc/pirlnode-env

/etc/systemd/system/pirlnode.service

cat /etc/pirlnode-env

you need to edit the file, with a file editor like:

vi, vim, joe, nano, pico

nano:

nano /etc/pirlnode-env

joe:

joe /etc/pirlnode-env


MASTERNODE="----------------------------------"

TOKEN="1111111111111111111111111111111111111111"

or like this:

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

PrimateCrypto thanks for your info.

