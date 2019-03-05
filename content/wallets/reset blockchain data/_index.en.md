---
title: How To Reset Blockchain Data
weight: 3
pre: "<b>3. </b>"
chapter: true
---
![](/images_headers/wallet.png)


## Introduction
This guide covers resetting blockchain data, i.e. deleting and re-syncing the PIRL Nautilus wallet chaindata.
The most likely situation requiring this is that your Pirl wallet is stuck loading or will not sync.
If this is the case, follow the follow guide to resolve the issue.

## Important note
NB: Before attempting this process, you should make a backup of your keystore data/PIRL wallet. A guide on how to do this is available here: [How to Backup Pirl Wallets](https://docs.pirl.io/en/wallets/backup-pirl-wallets/)

## Deleting the blockchain data
After ensuring you have backed up your keystore/wallet data securely, the remainder of the process is straight-forward, and goes as follows:

 * **Close Pirl Nautilus wallet**
 * **Locate & Delete Pirl chaindata**
 * **Re-Open Pirl chaindata**

### Locating the data
On Windows, this data is located at:

`C:\Users\*YourUsername*\AppData\Roaming\Pirl\pirl`

On Linux, it's located at:

`~/.pirl`

On MacOS X, it's located at:

`~/Library/Pirl`

## Summary
Your blockchain data should now be reset, which will typically resolve most wallet-related issues.
When you reopen the wallet, do note that it will have to download the blockchain data again, which may take some time.


---
Author(s):
Bigchrome

