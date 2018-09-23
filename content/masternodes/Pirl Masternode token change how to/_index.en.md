---
title: Pirl Masternode token change how to
weight: 5
disableToc: true
---

## Overview

This guide will help ypu change the token on the Masternode
**the one-click-masternode setup users will not have to do this!**


## How to change the token.

**Open Poseidon** [Poseidon](https://poseidon.pirl.io/accounts/masternodes-list-private/)

The Masternode TOKEN is found here:

On the left menu, click on Masternodes -> My masternodes. 
You will see next to the masternode you created earlier, the masternode token under "MN token".

![](content/masternodes/Pirl Masternode token change how to/images/Mn_token.jpg)


**log in too your vps**


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

disable and restart the new service:
```
systemctl disable pirlnode
systemctl restart pirlnode
```


---
Author(s):
_dptelecom

Contributor(s):

