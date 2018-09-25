---
title: Pirl Masternode Token Change
weight: 5
disableToc: true
---

## Overview

This guide will help you change the masternode token of your masternode. The masternode token and the user token comprise the 2 tokens each masternode service on a VPS. You can check your [user token on Poseidon](https://poseidon.pirl.io/accounts/settings/) by going clicking **Profile > Settings**.

> The one-click masternode setup users will usually not have to do this as the process can be initiated remotely by Poseidon


## How to Change the Token

The **Masternode Tokens** are found here: [Poseidon](https://poseidon.pirl.io/accounts/masternodes-list-private/)

On the left menu, click on **Masternodes > My masternodes**.
You will see next to the masternode you created earlier, the masternode token under **MN token**.

![](/masternodes/pirl masternode token change/images/mn_token_page.png)


**Log in to your VPS**

Update the file with your Masternode token in it.
Depending on how it was setup, it will be in one of the following files:

`/etc/pirlnode.env`

`/etc/pirl.env`

`/etc/pirlnode-env`

`/etc/systemd/system/pirlnode.service`

Find the file that's applicable in your situation and edit it. If you have more than 1 of the files listed above, we recommend disabling your masternode and setting up a new OneClick masternode to eliminate any future frustrations with manual updates.

To simply view the file you can execute:
> Note that below we keep using /etc/pirlnode-env only as an example of where your token information is located. You will need to update your file containing the MASTERNODE token.

```
cat /etc/pirlnode-env
```

Your file will look something like the one below.  You will have a **MASTERNODE** token and a **TOKEN** (a.k.a. **USER token**)
```
MASTERNODE=11111111-1111-1111-1111-111111111111
TOKEN=1111111111111111111111111111111111111111
```

> Note: You need to change the MASTERNODE token above. The bottom one is your user token and does not need to be changed.

You need to edit the file in question with a file editor like: **vi, vim, joe, nano, pico**

You can change it as follows using `nano`:

```
nano /etc/pirlnode-env
```

Make sure the **MASTERNODE** token matches the one you recorded online on [Poseidon](https://poseidon.pirl.io/accounts/masternodes-list-private/)
![](/masternodes/pirl masternode token change/images/mn_token.png)

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
