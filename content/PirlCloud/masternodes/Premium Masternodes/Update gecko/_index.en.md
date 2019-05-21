---
title: Manual Update to 1.8.27-gecko
weight: 3
pre: "<b>3. </b>"
chapter: true
---

{{< imagesurlsheaders "images_headers/Masternodes.png" >}}

## Manual Masternode Update to 1.8.27-gecko  
The instructions are intended for Redhat or CentOS based VPS but should work on most major Linux distributions.   
You may have the need to adjust the firewall instructions to match the software software running on your VPS.  
Login as root and update the system, then install dependencies:

## Binary:   
(marlin now the same for both types)  
https://storage.googleapis.com/pirl-node/pirl-1.8.27-gecko/marlin/marlin-masternode-gecko1_8_27
https://storage.googleapis.com/pirl-node/pirl-1.8.27-gecko/masternodes/content/pirl-linux-amd64-content
https://storage.googleapis.com/pirl-node/pirl-1.8.27-gecko/masternodes/premium/pirl-linux-amd64-premium  


## Update with script from @phatblinkie if not want to do it all Manual:

https://github.com/phatblinkie/mn_installer



## The update process:

Stop the  pirlnode service:

```
systemctl stop pirl

```

and stop the pirlmarlin service:

```
systemctl stop marlin

```




### Download the premium masternode binaries:
```
wget https://storage.googleapis.com/pirl-node/pirl-1.8.27-gecko/masternodes/premium/pirl-linux-amd64-premium
wget https://storage.googleapis.com/pirl-node/pirl-1.8.27-gecko/marlin/marlin-masternode-gecko1_8_27

```

### Download the content node binaries:

```
wget https://storage.googleapis.com/pirl-node/pirl-1.8.27-gecko/masternodes/content/pirl-linux-amd64-content
wget https://storage.googleapis.com/pirl-node/pirl-1.8.27-gecko/marlin/marlin-masternode-gecko1_8_27

```


Move the main binary to /usr/bin/pirl For premium masternodes:  

```
mv pirl-linux-amd64-premium /usr/bin/pirl

```

For content nodes:  
```
mv pirl-linux-amd64-content /usr/bin/pirl

```

Move the marlin binary to /usr/bin/marlin  For premium masternodes and content nodes:  

```
mv marlin-masternode-gecko1_8_27 /usr/bin/marlin

```

To grant Permission :

```
chmod 0755 /usr/bin/pirl
chmod 0755 /usr/bin/marlin

```


### Now reboot the vps.
```
reboot
```


Watch the masternode process synchronize with the blockchain:
```
journalctl -f

```

Once messages like the following are displayed, your masternode is now synchronized and contributing to the network.

```
  ########  masternode sending proof of activity to poseidon for block  3625046  please check poseidon.pirl.io for details  //  marlin version is gecko #########

```

Monitoring
We don’t encourage active access on the server. If, however, you wish to check the status, log into your server and issue the following command:  
```
journalctl -f
```

Monitor the status of your masternode by checking the Poseidon Masternode Details page. A functioning node should appear as follows, although the version may be different than what is shown in the screen shot below.

{{% notice warning %}}
In case synchronisation does not work follow these steps to remove the database:
{{% /notice %}}  

- First export the tokens:

```
export MASTERNODE=fzeffz-zefzef-zefze-zefze-zefzef-zefzef <<<---YOUR TOKEN GOES HERE
export TOKEN=zfzefezfzefzecfzegregkgeorgoerbvnijv <<<---YOUR TOKEN GOES HERE


```

that step above can also be done,
if you have this file /etc/pirlnode-env,
you can do:  
```
. /etc/pirlnode-env && export MASTERNODE TOKEN

```


- And then remove the database:  

```
pirl removedb

```

or the last resort way:  

```
rm -rf /root/.pirl

```



Kind regards,  
PirlTeam.  

---
Author(s):


The Pirl Team


Contributor(s):


@Dptelecom
