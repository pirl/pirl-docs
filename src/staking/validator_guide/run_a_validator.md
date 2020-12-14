# Validator




Validators secure the Relay Chain by staking PIRL, validating proofs from collators and participating in consensus with other validators.

These participants will play a crucial role in adding new blocks to the Relay Chain and, by extension, to all parachains. This allows parties to complete cross-chain transactions via the Relay Chain.

Validators perform two functions. First, verifying that the information contained in an assigned set of parachain blocks is valid (such as the identities of the transacting parties and the subject matter of the contract). Their second role is to participate in the consensus mechanism to produce the Relay Chain blocks based on validity statements from other validators. Any instances of non-compliance with the consensus algorithms result in punishment by removal of some or all of the validator’s staked PIRL, thereby discouraging bad actors. Good performance, however, will be rewarded, with validators receiving block rewards (including transaction fees) in the form of PIRL in exchange for their activities.

## Top 100
Currently, there are only 100 slots available for validators. When all slots are taken, the race for being a validator start.
The network only pick the top 100 validator in term of total stakes (validator stake + nominators stake)

At this point, it's important for validator to have some nominators who support them with their own stake to grow the total stake and be in the top 100.
The validors that not in the top 100 will not be elected by the network and **do not receive any reward**. 

<p align=right> Written by Masterdubs & WeHaveCookie </p>
