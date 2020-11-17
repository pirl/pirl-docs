# Migration FAQ


#### We have until when to claim for yours Pirl 2.0 ?

>There is no time limit set.


#### Do I need to disable the masternode to get my claim in Pirl 2.0 ?
> No, you will get your coins even if they are locked in the contract.

#### Does wPIRL need to be bridged back to pirl legacy chain for swap of coins? 
> Yes, you need to bridge all your coins back to be able to swap your PIRL. After the snapshot it's not possible until we re-implemented it. No date or schedule yet.

#### Is Ledger or any hardware wallet supported at the start of the new chain ? 
> Not at the beginning but we will support hardware wallets at a later stage. No date or schedule yet.

#### If I keep my PIRL on the exchange, is the change to the new blockchain automatic ?
> Yes, the exchanges will swap your PIRL automatically. (Please don´t hold your coins longer at any exchange, not your keys, not your coins)

#### What should I do to switch to pirl 2.0 ?
> The change will be at block 7 650 000. Follow information on Discord and Twitter on when you will be able to perform the swap and switch to Pirl 2.0

#### How will the swap work ?
> Snapshot will be taken at block 7 650 000, and you will be able to swap the Pirl balance at this block to Pirl 2.0

#### Where and how to apply for coins ?
> From Pirl 2.0 Portal after block 7 650 000. Follow [this tutorial](https://community.pirl.io/t/claim-pirls-from-old-chain-to-pirl-2-0-tutorial/131)

#### What is the minimum requierement for a validator ?
> *The absolute minimum requrements to run the validator node are described below. This settings are NOT recomended as this could lead to unstable node and you could end up getting slashed!! If running validator node with specs close to minimum you must monitor your node and set up warnings for load etc..*
>
>* Minimum: 10 GB RAM, 60 GB Storage, 4 CPU 
>* Recomended: 60 GB RAN, 300 GB Storage, 6 CPU
>* Public IP on validator node needed for basic setup. 
(More information will come on how to setup a secure validator with sentry nodes)
>* Stabile internet connection are required. The validator nodes plays a very important role by securing the network and we recommend renting VPS from providers with good infrastructure and not trying to set up at home. 
> ### [Read more about validators requierements here](../validator_guide/guides_how_to_validate.md) 

#### How does slashing works ?
> - Level 1: isolated unresponsiveness, i.e. being offline for an entire epoch. No slashing, only chilling.
>- Level 2: concurrent unresponsiveness or isolated equivocation. Slashes a very small amount of the stake and chills.
>- Level 3: misconducts unlikely to be accidental, but which do not harm the network's security to any large extent. Examples include concurrent equivocation or isolated cases of unjustified voting in GRANDPA. Slashes a moderately small amount of the stake and chills.
>- Level 4: misconduct that poses a serious security or monetary risk to the system, or mass collusion. Slashes all or most of the stake behind the validator and chills.
>
>[Reference research article about slashing](https://research.web3.foundation/en/latest/polkadot/slashing.html)

#### I used the web wallet, I'm safe for the claim ?
> Yes, just wait the fork of the chain and you will be able to claim your coins in Pirl 2.0.

#### Can I claim my coins with ledger wallet ?
> Yes, be sure to have backup phrase and latest firmware.

#### I didn't unlocked the coins locked in masternode contract, are they lost ?
> No, the coins locked in the masternode contract(s) will be available freely in your wallet after the fork in the new network.

#### What is the validator reward amount ?
> We can calculate it precisely, it depend on the network staking rate. Validator will have minted coins plus 20% of the transfert fees ( 80% goes to decentralised treasury ). Rewards are calculated based on era points, which have a probabilistic component. In other words, there may be slight differences in your rewards from era to era, and even amongst validators in the active set at the same time. These variations should cancel out over a long enough timeline.

#### Can I get my coins back if I stake or create a validator ?
> Yes you can unlock them when you want, you will have to wait the cooldown period to get it credited in your wallet, actual waiting period is 28 days.

### How to delete all the old Pirl services on masternodes ?
> BE SURE TO NOT HAVE PIRL KEYS PRESENT 

> ``` service pirl stop && service marlin stop && rm -rf /root/.pirl && rm -rf /root/.marlin && systemctl disable pirl && systemctl disable marlin ```