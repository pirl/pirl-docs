---
title: How to Backup Pirl Wallets
weight: 2
pre: "<b>2. </b>"
chapter: true
---
{{< imagesurlsheaders "images_headers/wallet.png"  >}}


## Overview
This is a guide for best practices in backing up your Pirl wallets, and for keeping your Pirl safe and secure.

## Introduction
So, you've just picked up a bundle of Pirl, you're in this for the long haul, and you're going to keep these coins for a long time. How can you make sure you don't lose access through fire/theft/crashes?
It's important to back up your Pirl wallets to ensure that any one failure won't result in you losing your Pirl. This guide will walk through best practice for backups and will touch on three platforms/options for doing so.

## Important to understand: What *is* a wallet?
At its core, the part of the wallet that gives you access to your funds and allows you to spend your coins, are your private keys. Your Pirl is stored on the blockchain, and the private keys are what unlock your funds and allow them to be sent. These private keys can be seen in a number of different forms, with the *raw* form being a string of 64 hexadecimal characters that looks something like:
```c6cbd7d76bc5baca530c875663711b947efa6a86a900a9e8645ce32e5821484e```

The importance of your private keys is two-fold. They give you access to your funds, but they will also give anyone with the key access to your funds too. For that reason it is IMPERATIVE that you take steps to protect these private keys and to keep them backed up.
The following section details common methods for storing these private keys, and the best practice for each.

## Wallet types and best practice
For a transaction to be approved, it always has to be signed with your private key. However, for additional functionality such as protecting the key with a password, there are various formats for storing your private key.

The most commonly used wallet types are as follows:

 * **Private Key (unencrypted)**
 * **Keystore (UTC/JSON) file.**
 * **Hardware wallets (e.g. Ledger/Trezor)**

### Private key (unencrypted)
This is the unencrypted text version of your private key. It does not require your password.
If someone else has this key, they can access your wallet without a password.
This makes this method of storage both the most simple and the most volatile.

#### Saving your private key as a Paper Wallet or Keystore file
It is typically recommended to use an encrypted version, however you should print a paper wallet and save this key somewhere offline.
There is a useful feature on https://wallet.pirl.io that allows you to export your wallet info as either a Keystore (JSON/UTC) file, or to print a paper wallet.

Simply click on the "View Wallet Info" tab
{{< imagesurlsheaders "cloud/main_pirl_wallet_page_view_wallet_highlight.png" >}}

Input your wallet details in whichever format you have them
{{< imagesurlsheaders "cloud/view_wallet_details_landing_page.png" >}}


Your wallet details will then be presented as public/private key, with the option to both generate a Keystore (JSON/UTC) file, or to print a paper wallet.
{{< imagesurlsheaders "cloud/view_wallet_details.png" >}}

The paper wallet will look like this
{{< imagesurlsheaders "cloud/paper_wallet_example.png" >}}

You should print the paper wallet twice, and store it in two secure locations. Treat it like cash.
You should also download the keystore file and save it to an external medium such as a USB drive or Hard drive. It's best practice to have a backup in multiple physical locations should the worst happen.
Always remember the golden rule of backups: "Two backups is one, and one is none."

### Keystore (UTC/JSON) file.
This is the recommended version to save, and is also the format in which the Pirl Nautilus (Desktop) Wallet stores your wallet.
Since the keystore format matches that used by the web wallet at https://wallet.pirl.io, you can easily import in either direction.

This file is encrypted by the password you chose when you create the file.

You should save the keystore file to an external medium such as a USB drive or Hard drive. It's best practice to have a backup in multiple physical locations should the worst happen.

#### Backing up your Nautilus Wallet

To backup your Nautilus Wallet, click **File** > **Backup** > **Accounts**
{{< imagesurlsheaders "cloud/nautilus_backup.png" >}}


This will open the appdata folder containing your wallet files
{{< imagesurlsheaders "cloud/nautilus_backup_folder.png" >}}


### Hardware Wallets
Hardware wallet support for Pirl is available on both Ledger and Trezor devices.
These devices present a secure way to store and access your funds, with the private keys being stored in a protected area of the device which prevents them from being transferred out of the device in plaintext format.
This method means that even if your computer is compromised, you should be able to sign transactions in a secure fashion.
As with all technology, there are advanced means to attack these devices that can potentially expose your funds, but this is beyond the scope of this article and not something the average user needs to concern themselves with.

One particular security precaution that should be taken, however, is to only purchase these devices through first-party or trusted stores, and to ensure the device has not been opened or otherwise tampered with when you receive it.


## Summary
In summary, the most important actions to secure your Pirl:

 * Use a hardware wallet if possible, password protected keystore (UTC/JSON) being the next best option.
 * Use the pirl web wallet to save a paper wallet and print this twice, keeping it in two secure locations.
 * No matter which wallet format you use, make multiple backups in multiple locations.
 * Never expose your private keys to any (untrusted) third party, as this will give them full access to your funds.


---
Author(s):
Bigchrome
