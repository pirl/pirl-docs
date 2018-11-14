---
title: Updating Pirl Masternode binary Manually
weight: 9
pre: "<b>9. </b>"
chapter: true
---

## Overview

Running a PIRL masternode requires the use of a Virtual Private Server (VPS) with a static public IP address directly assigned to an interface.


## Prerequisites

* **A VPS with minimum 4GB Total OS RAM minimum (more is recommended), enough storage to run the masternode (Minimum 20GB, Recommended 60GB+), and a Public IP assigned at the network interface**
 - The official requirements are: 4GB RAM, 20GB space, 3TB transfer, public IPv4 IP. Once you order your VPS, you will receive its root credentials. The easiest path forward is to only use this VPS for your Pirl Masternode and give Poseidon your root credentials so it can manage and update your VPS.




## Updating Pirl Masternode binary Manually

The instructions are intended for Redhat or CentOS based VPS but should work on most major Linux distributions.


Login as root and update the system, then install dependencies:
```
yum update
sudo yum install wget systemd -y
```



Create a `pirl` user and add it to the `systemd-journal` group:
```
adduser pirl && passwd pirl
usermod -aG systemd-journal pirl
```

Download the premium masternode binaries:
```
wget https://git.pirl.io/community/pirl/uploads/7b62da3dc3ce36b97ad8a04ee6ed67a0/marlin-v5-masternode-premium-hulk
wget https://git.pirl.io/community/pirl/uploads/f991222e04b2525cfb4a94a078f7247b/marlin-v5-masternode-premium-hulk
```

...or the content node binaries:
```
wget https://git.pirl.io/community/pirl/uploads/2f5b3ad72e4a2d747ca3cfebb0715077/marlin-v5-masternode-content-hulk
wget https://git.pirl.io/community/pirl/uploads/7b44acaa183a620bd1e57c1663ee9b72/marlin-v5-masternode-content-hulk
```

Mark them executable, and change the owner to `pirl:pirl`:

For premium masternodes:
```
chmod 755 pirl-v5-masternode-premium-beta
chmod 755 marlin-v5-masternode-premium-beta
chown pirl:pirl pirl-v5-masternode-premium-beta
chown pirl:pirl marlin-v5-masternode-premium-beta
```

For content nodes:
```
chmod 755 pirl-v2-masternode-content-beta
chmod 755 marlin-v2-masternode-content-beta
chown pirl:pirl pirl-v2-masternode-content-beta
chown pirl:pirl marlin-v2-masternode-content-beta
```

Move the main binary to `/usr/sbin/pirl-geth`:

For premium masternodes:
```
mv pirl-v5-masternode-premium-beta /usr/sbin/pirl-geth
```

For content nodes:
```
mv pirl-v2-masternode-content-beta /usr/sbin/pirl-geth
```


Move the marlin binary to `/usr/sbin/pirl-marlin`:

For premium masternodes:
```
mv marlin-v5-masternode-premium-beta /usr/sbin/pirl-marlin
```

For content nodes:
```
mv marlin-v2-masternode-content-beta /usr/sbin/pirl-marlin
```


Create a system service file for the geth service:
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
ExecStart=/usr/sbin/pirl-geth --rpc --ws

[Install]
WantedBy=default.target pirlmarlin.service
```


Create a system service file for the marlin service:
```
vi /etc/systemd/system/pirlmarlin.service
```

Press the `i` button to enter insertion mode, then add the following.  Be sure to add your own MASTERNODE and user TOKEN to the Environment under the `[Service]` section:
```
[Unit]
Description=Pirl Client -- marlin content service
After=network.target pirlnode.service

[Service]
Environment=MASTERNODE=YoUR MaSTErNodE ToKEn GoES HeRE
Environment=TOKEN=YoUR UsER ToKEn GoES HeRE

User=pirl
Group=pirl
Type=simple
Restart=always
RestartSec=30s
ExecStartPre=/bin/sleep 5
ExecStart=/usr/sbin/pirl-marlin daemon

[Install]
WantedBy=default.target
```

Enable and start the pirlnode service:
```
systemctl enable pirlnode
systemctl restart pirlnode
```

Become the `pirl` user, then initialize Marlin.  If you're currently logged in as root, do the following:
```
su pirl
/usr/sbin/pirl-marlin init
exit
```

Enable and start the pirlmarlin service:
```
systemctl enable pirlmarlin
systemctl restart pirlmarlin
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
@Dptelecom


Contributor(s):

