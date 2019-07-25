---
title: PirlGuard
weight: 6
pre: "<b>6. </b>"
chapter: true
---

{{< imagesurlsheaders "images_headers/pirlguard.png"  >}}


## PirlGuard - Innovative Solution against 51% Attacks


<iframe width="560" height="315" src="https://www.youtube.com/embed/Q-f01eFYlig" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


Pirl block 2,442,442 is a historical event not only for Pirl but for blockchain security in general.


As most of the Pirl community is aware the Pirl Team been researching different ways to secure our blockchain against both ASICS and 51% attacks for several months, openly within our Discord and behind the scenes. During this time Pirl fell victim to a 51% attack along with many other blockchains.



{{< imagesurlsheaders "cloud/1.png" >}}




One of the contributing threat factors that has recently made nearly all PoW consensus mechanism Blockchains susceptible to 51% attacks has been the decline of mining profits leading to excess amounts of cheap hash power.


Most sources available explain the complexity of those attacks and showcase PoS and 3rd party solutions as a good measure for protecting against such attacks. One solution would involve rolling back the blockchain which would still harm the miners, investors, and holders of Pirl. While a PoS consensus mechanism is also vulnerable other kinds of attacks such as “Nothing-At-Stake” attack.


After thorough research and analysis of blockchain security methods the Pirl team did not view any of the currently available options as acceptable long-term preventable measures against these types of attacks. This left the team with the only possible choice available, to develop a new Security Protocol.


In order to understand the PirlGuard Protocol including the how and why behind Pirl developing the innovative solution, you must understand how a 51% attack works. If you are confident in your knowledge regarding the anatomy of a 51% attack feel free to skip to the“How PirlGuard works?” section of this article.


## How a 51% attack works


Source: [CoinMonks](https://medium.com/coinmonks/what-is-a-51-attack-or-double-spend-attack-aa108db63474)


Author: [Jimi.S](https://twitter.com/JimiSinnige)


When a Bitcoin owner signs off on a transaction, it is put into a local pool of unconfirmed transactions. Miners select transactions from these pools to form a block of transactions. In order to add this block of transactions to the blockchain,
they need to find a solution to a very difficult mathematical problem. They try to find this solution using computational power. This is called hashing.
The more computational power a miner has, the better their chances are to find a solution before other miners find theirs. When a miner finds a solution,
it will be broadcasted (along with their block) to the other miners and they will only verify it if all transactions inside the block are valid according to the existing record of transactions on the blockchain.
Note that even a corrupted miner can never create a transaction for someone else because they would need the digital signature of that person in order to do that (their private key).
Sending Bitcoin from someone else’s account is therefore simply impossible without access to the corresponding private key.


## Stealth mining — creating an offspring of the blockchain


Now pay attention. A malicious miner can however, try to reverse existing transactions. When a miner finds a solution, it is supposed to be broadcasted to all other miners so that they can verify it whereafter the block is added to the blockchain (the miners reach consensus). However, a corrupt miner can create an offspring of the blockchain by not broadcasting the solutions of his blocks to the rest of the network. There are now two versions of the blockchain.



{{< imagesurlsheaders "cloud/2.png" >}}



There are now two versions of the blockchain. The red blockchain can be considered in ‘stealth’ mode.


One version that is being followed by the uncorrupted miners, and one that is being followed by the corrupted miner. The corrupted miner is now working on his own version of that blockchain and is not broadcasting it to the rest of the network. The rest of the network doesn’t pick up on this chain, because after all, it hasn’t been broadcasted. It is isolated to the rest of the network. The corrupted miner can now spend all his Bitcoins on the truthful version of the blockchain, the one that all the other miners are working on. Let’s say he spends it on a Lamborghini for example. On the truthful blockchain, his Bitcoins are now spent. Meanwhile, he does not include these transactions on his isolated version of the blockchain. On his isolated version of the blockchain, he still has those Bitcoins.



{{< imagesurlsheaders "cloud/3.png" >}}


Meanwhile, he is still picking up blocks and he verifies them all by himself on his isolated version of the blockchain. This is where all trouble starts… The blockchain is programmed to follow a model of democratic governance, aka the majority. The blockchain does this by always following the longest chain, after all, the majority of the miners add blocks to their version of the blockchain faster than the rest of the network (so; longest chain = majority). This is how the blockchain determines which version of its chain is the truth, and in turn what all balances of wallets are based on. A race has now started. Whoever has the most hashing power will add blocks to their version of the chain faster.



{{< imagesurlsheaders "cloud/4.png" >}}



## A race — reversing existing transactions by broadcasting a new chain


The corrupted miner will now try to add blocks to his isolated blockchain faster than the other miners add blocks to their blockchain (the truthful one). As soon as the corrupted miner creates a longer blockchain, he suddenly broadcasts this version of the blockchain to the rest of the network. The rest of the network will now detect that this (corrupt) version of the blockchain is actually longer than the one they were working on, and the protocol forces them to switch to this chain.



{{< imagesurlsheaders "cloud/5.png" >}}


The corrupted blockchain is now considered the truthful blockchain, and all transactions that are not included on this chain will be reversed immediately. The attacker has spent his Bitcoins on a Lamborghini before, but this transaction was not included in his stealth chain, the chain that is now in control, and so he is now once again in control of those Bitcoins. He is able to spend them again.



{{< imagesurlsheaders "cloud/6.png" >}}



*This is a double-spend attack.*
It is commonly referred to as a 51% attack because the malicious miner will require more hashing power than the rest of the network combined (thus 51% of the hashing power) in order to add blocks to his version of the blockchain faster, eventually allowing him to build a longer chain.


Now that we know how the attack works we can summarize it in a few key moments.


A) The attacker needs to mine his own version of the blockchain in private with hashrate greater than the one on the main network in order to be faster and create a longer chain. This is often a race for getting a chain with 10–20–50 blocks longer.


B) Once he is in possession of a longer blockchain he needs to broadcast it to the network. Then the network needs to recognize it as the longest chain and accept it.


C) A successful double spend would orphan the initial transactions making the coins available in the attacker wallet once again after the applied longer chain.


## How PirlGuard works?


In order to disrupt the mechanics behind 51% attack that allows an attacker to be successful, we have deployed a core solution with a modified consensus algorithm that will defend our blockchain and many others in the near future from virtually all 51% attacks.


## PirlGuard System
With the PirlGuard Protocol deployed the chances of an attack succeeding are vastly reduced. As we know once the attacker has created a longer chain through privately mining a separate chain they will then have to broadcast it to the network. Once the attacker opens their node for peering it will attempt to peer with rest of the nodes on the network, telling them that they are wrong. However, once this happens PirlGuard will drop the peer and penalize them by sentencing them to mine X amount of penalty blocks due to their un-peered mining. The amount of penalty blocks assigned depends on the amount of blocks that the malicious miner mined in private.



{{< imagesurlsheaders "cloud/7.png" >}}


The PirlGuard security protocol greatly deters attackers from attempting malicious peering giving the main network a much needed boost in security. This new security mechanism reduces the chances to approximately 0.03%.


But, this is not the only security measure we have prepared.


## Masternode operated notary contracts on multiple blockchains and monitoring system.


The masternodes will take upon a new role altogether with their other utility functions. They will notarize the blockchain and be allowed to act in the processes of penalizing bad actors and preserve honest consensus on the Pirl blockchain.


In case an attacker is still determined to apply a large amount of funds and resources to attempt their luck(0.03% chance), and somehow succeeds to enforce a longer chain onto the network a newly initialized orphan monitoring system will detect the reorganizations of orphaned blocks which will alert the team to take necessary actions and countermeasures.


As additional safety measure the notary contract will be deployed both on Pirl and Ethereum blockchains.


## Increasing the amount of required confirmations for exchanges.


An additional measure that will be implemented is a higher requirement of block confirmations on exchanges to validate deposits. Another step towards making an attack close to impossible and not even worth an attackers time.


##  Open Source


Pirl has so far contributed to blockchain by developing the first Ethash code based masternode network, the first private IPFS implementation running over a masternode network and is currently working on their own private encrypted blockchain storage solution.
The PirlGuard Security Protocol will be added to our open source library along with the core of the project.
At Pirl we are developing to revolutionize and streamline blockchain technology for the entire blockchain industry. This means our code will be available to anyone to study, educate, test, modify or apply towards their own blockchain network security against future 51% attacks.


[Source Code:](https://git.pirl.io/community/pirl)
[Website:](https://pirl.io/en)






#PirlTogetherStrong


Yours,

Pirl Team


---
Author(s):  


@Fawkes

Contributor():


@dptelecom
