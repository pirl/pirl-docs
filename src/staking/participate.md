# Particiapte in Pirl 2.0


# Nominator	

Nominators are one type of participant in the staking subsystem of Pirl.<br> 	
They are responsible for appointing their stake to the validators who are the second type of participant. By appointing their stake, they are able to elect the active set of validators and share in the rewards that are paid out.	

While the validators are active participants in the network that take part in the block production and finality mechanisms, nominators take a more passive role with a "set-it-and-forget-it" approach. Being a nominator does not require running a node of your own or worrying about online uptime. However, a good nominator performs due diligence on the validators that they elect. When looking for validators to nominate, a nominator should pay attention to their own reward percentage for nominating a specific validator - as well as the risk that they bare of being slashed if the validator gets slashed.	

## Before you start nominating	
Do some research before you start, take your time and read the guidence given to make sure that you are getting the most out of your stake and with less risk.	

**Some tips before you start:**<br>	
* Nominate validators with an identity.<br>	
-Known staking services/teams or community members are more likely to be active and keep their Validator online. Some services/teams has their own Discord channels as well.	
* Check history of validator. <br>	
-Performance history are available by clicking on the green chart symbol in the <a href="https://explorer.pirl.network/#/staking" target="_blank">staking list</a>	
* Check "own stake" of validator.<br>	
-If validator missbehaves it can be slashed and loose some or all of its own stake and nominators stake. Validators with higher stake have a higher risk and are more likely to monitor the node carefully.	
* Nominate more then one validator.<br>	
-You are able to choose up to 16 different validators. The network will choose the validator that gives the best return. You can select validators on the wait list as well, and the system will change to any of them when they are choosen to be a active validator.	
* Check validators "commission".<br>	
-Validators are able to set a "commission fee" as a service charge for running the node and VPS cost. Validators with 100% commission will take all of the Pirl reward !	

### Follow the guide for "[How to be a Nominator](nominator_guide/how_to_nominate.md)" when you are ready to start nominating.

# Validator

Validators secure the Relay Chain by staking PIRL, validating proofs from collators and participating in consensus with other validators.

These participants will play a crucial role in adding new blocks to the Relay Chain and, by extension, to all parachains. This allows parties to complete cross-chain transactions via the Relay Chain.

Validators perform two functions. First, verifying that the information contained in an assigned set of parachain blocks is valid (such as the identities of the transacting parties and the subject matter of the contract). Their second role is to participate in the consensus mechanism to produce the Relay Chain blocks based on validity statements from other validators. Any instances of non-compliance with the consensus algorithms result in punishment by removal of some or all of the validator’s staked PIRL, thereby discouraging bad actors. Good performance, however, will be rewarded, with validators receiving block rewards (including transaction fees) in the form of PIRL in exchange for their activities.

## Top 100
Currently, there are only 100 slots available for validators. When all slot are taken, the race for being a validator start.
The network only pick the top 100 validator in term of total stakes (validator stake + nominators stake)

At this point, it's important for validator to have some nominators who support them with their own stake to grow the total stake and be in the top 100.
The validors that not in the top 100 will not be elected by the network and **do not receive any reward**. 

### Follow the guide for "[Run a validator](validator_guide/guides_how_to_validate.md)" when you are ready to start validating.

## Other staking topic 
### [How to be unbound](nominator_guide/how_to_unbound.md)
### [How payout works](./payout.md)

<p align=right> Written by Masterdubs & FanThomas & WeHaveCookie </p>