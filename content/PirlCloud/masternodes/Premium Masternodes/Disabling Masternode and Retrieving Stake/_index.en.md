---
title: Retrieve Masternode Stake
weight: 2
pre: "<b>2. </b>"
chapter: true
---
{{< imagesurlsheaders "images_headers/Masternodes.png"  >}}


## Overview

At any time, you can run two masternode contract functions and retrieve your 20,000 PIRL stake back into your wallet.

## Disabling Masternode and Retrieving Stake

**Open Nautilus** and navigate to the **Contract** tab located at the top right corner.

You should see the masternode contract on the left side. It will have the address of `0x256b2b26Fe8eCAd201103946F8C603b401cE16EC`. Select this address.
(NOTE: If you don't have a contract showing in the **watch contract** section, you can add it as described in the next section.)

On the right side, the contract function menu will be shown.

Select the **Disable Node** function, then the wallet associated with the contract and hit **Execute**

![](/PirlCloud/masternodes/images/disable-node.png)

On the next screen, confirm you have enough **gas** for the transaction, enter your **UTC file password** and hit **Send Transaction**.

![](/PirlCloud/masternodes/images/disable-node2.png)

Allow 30-60 seconds before running the next step.

Select the **Withdraw Stake** function, then the wallet associated with the contract and hit **Execute**

![](/PirlCloud/masternodes/images/withdraw-stake.png)

On the next screen, confirm you have enough **gas** for the transaction, enter your **UTC file password** and hit **Send Transaction**.

![](/PirlCloud/masternodes/images/disable-node2.png)

### Not Enough gas

Sometimes the wallet will be unable to automatically calculate the gas needed for a transaction and will automatically set it to 0. In this situation, you can manually adjust the gas by clicking on where it says 0 and write in your own amount.  A good amount of gas for this purpose is **121,000**.

![](/PirlCloud/masternodes/images/confirm-gas.png)

## Adding Masternode Contract in Nautilus

**Open Nautilus** and navigate to the **Contract** tab located at the top right corner.

![](https://cdn-images-1.medium.com/max/1600/0*OW_7W9P_u0k7ZdmZ.png)

Once there, click on the **Watch Contract** button.

![](https://cdn-images-1.medium.com/max/1600/0*wZbZlfAdjrUuhr53.png)

For **Contract Address** fill in `0x256b2b26Fe8eCAd201103946F8C603b401cE16EC`. The **Contract Name** can be anything you’d like.  And lastly, the **JSON Interface field** needs to be populated with:

```
[{"constant":false,"inputs":[],"name":"nodeRegistration","outputs":[{"name":"paid","type":"bool"}],"payable":true,"stateMutability":"payable","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getNodeAddress","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"","type":"address"}],"name":"moderators","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"","type":"address"}],"name":"nodes","outputs":[{"name":"pirlAddress","type":"address"},{"name":"nodeStake","type":"uint256"},{"name":"nodeHash","type":"bytes20"},{"name":"stakeLocked","type":"bool"},{"name":"nodeEnabled","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"disableNodeRegistration","outputs":[{"name":"disabled","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"nodeCost","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getStakeLockedStatus","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"nodeCount","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[{"name":"_admin","type":"address"}],"name":"setAdmin","outputs":[{"name":"set","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"owner","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"enableNode","outputs":[{"name":"enabled","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[],"name":"nodeRegistrationEnabled","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"disableNode","outputs":[{"name":"disabled","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":false,"inputs":[],"name":"withdrawStake","outputs":[{"name":"withdrawn","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[{"name":"","type":"uint256"}],"name":"nodeAddresses","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getNodeEnabledStatus","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getNodeStake","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[],"name":"enableNodeRegistration","outputs":[{"name":"enabled","type":"bool"}],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[{"name":"_pirlAddress","type":"address"}],"name":"getNodeHash","outputs":[{"name":"","type":"bytes20"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"nodeFee","outputs":[{"name":"","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[],"name":"admin","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"inputs":[],"payable":false,"stateMutability":"nonpayable","type":"constructor"},{"payable":true,"stateMutability":"payable","type":"fallback"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_nodeRegistered","type":"bool"},{"indexed":false,"name":"_dateRegistered","type":"uint256"}],"name":"MasterNodeRegistered","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_nodeDisabled","type":"bool"},{"indexed":false,"name":"_dateDisabled","type":"uint256"}],"name":"MasterNodeDisabled","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_nodeEnabled","type":"bool"},{"indexed":false,"name":"_dateEnabled","type":"uint256"}],"name":"MasterNodeEnabled","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_nodePaid","type":"bool"},{"indexed":false,"name":"_datePaid","type":"uint256"}],"name":"MasterNodeRewarded","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_pirlAddress","type":"address"},{"indexed":true,"name":"_nodeHash","type":"bytes20"},{"indexed":true,"name":"_stakeWithdrawn","type":"bool"},{"indexed":false,"name":"_dateWithdrawn","type":"uint256"}],"name":"StakeWithdrawn","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_invoker","type":"address"},{"indexed":false,"name":"_dateEnabled","type":"uint256"},{"indexed":true,"name":"_registrationEnabled","type":"bool"}],"name":"MasterNodeRegistrationEnabled","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_invoker","type":"address"},{"indexed":false,"name":"_dateDisabled","type":"uint256"},{"indexed":true,"name":"_registrationDisabled","type":"bool"}],"name":"MasterNodeRegistrationDisabled","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_invoker","type":"address"},{"indexed":true,"name":"_admin","type":"address"},{"indexed":true,"name":"_adminSet","type":"bool"}],"name":"SetAdmin","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"_invoker","type":"address"},{"indexed":true,"name":"_newOwner","type":"address"},{"indexed":true,"name":"_ownerChanged","type":"bool"}],"name":"TransferOwnership","type":"event"}]

```



---
Author(s):
@dptelecom
Contributor(s):
