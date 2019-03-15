---
title: Roundtable 2018-09-22
weight: 50
pre: "<b>1. </b>"
chapter: true
---

{{< imagesurlsheaders "images_headers/round_table.png" >}}



## TL;DR ##
The PIRL Marlin content masternode binaries are out for testing!

## 2018/09/22 - Content Masternodes are out for testing! ##
This time masterdubs (PIRL founder) announced 1 day before the meeting that the community should
expect something exciting in a
[tweet](https://twitter.com/mast3rdubs/status/1041304582796795905) as well as in day-to-day interactions on Discord.

The meeting was started by masterdubs (dubs for short) with a quick comment that the community was expecting an announcement about something which came to be known as Marlin. Marlin is the next iteration of the masternode products released by the PIRL team.

> Marlins in nature are known as fast swimmers. As such, by the name Marlin, dubs aims to capture the same effect within the content masternode replication arena.

Dubs says that questions are welcome... but not about Marlin! The chatroom explodes with activity. He also mentions that he will sleep for a week after the successful release of Marlin.

> The community can attest that dubs is one of the hardest working devs, always active, at any all odd hours. Many irons in the fire keeping with mind awake with excitement.

After another moment of activity in the chatroom, some questions thrown out, dubs mentions that maybe today will be the day people will be able to run Marin. Marlin is out, everything is ready for real world testing, he announces!

```
daxm: Docs on how to install Marlin?
```
Dubs: Marlin will be automatically pushed using Poseidon (automation = better!) and he also confirms that soon documentation will be released on how to use Marlin.

```
mk: Can premium masternodes run marlin without additional stake?
```
>> mk is a respected and knowledgeable developer who took an interest in the PIRL community project.

Dubs: I want to be really clear, all premium masternodes will be required to run all 3 (premium, content & storage) binaries for redundancy purposes.

He makes is clear that the masternodes are expected to perform service for the network and as such, requiring ample resources.

```
mk: What does a 10K stake get us? that is smaller node without geth?
```
Dubs: No, it [Marlin] will run geth and it will talk to to the geth node with a contract.

```
Phatblinkie: Can subdomains work?
```
Dubs: Yes & also the goal is to put TLS on it.

```
mk: so am I correct - it makes no sense to split the 20k masternode to 2 10k nodes?
```
Dubs: No, premium will always be more because it will receive part of the PIRL Marketplace fees and part of the Content and Storage nodes rewards, as needed to augment the network (note: reason why premium is required to run all 3 binaries, see above).

```
daxm: Will each MN "function" require its own cert or one cert for the whole MN?
```
Dubs: Only 1 cert for all functions.

```
mk: some of us are running multiple nodes per a single masternode token, due to (poseidon issue?) ....  
```
Dubs: The problem is the Poseidon server cluster which is running high on memory. I'm working on adding more capacity to it in the next few days. I will talk to you more about it in private.

```
General Mayhem: When pirltube?
```
Dubs: In a week or two. Once enough beta testers run Marlin, we will be able to run PirlTube on the new masternodes.

```
mk: Will be be able to run multiple MNs for redundancy with the new Marlin masternodes?
```
Dubs: Yes, that will not change.

Dubs also mentions that the PIRL team will grow once the Marlin masternode is out and PirlTube is in use.

```
blck: Is there data redundancy if one node is out?
```
Dubs: Yes blck. I want to put Marlin is a sidechain to completely decentralize it. At first we will test the database, then content replication.

Dubs says he wants to create a community based marketing team. If anyone is interested, write a proposal and submit it to him directly.

```
blck: the data on the content masternode is encrypted?
```
Dubs: No, I don't see any reason. If someone deletes data maliciously, the other replicas will have it.

```
Wracul: Q: regarding the PirlTube. Someone mentioned that you can only access it though PirlApp.
```
Dubs: Yes, only PirlApp at first

```
daxm: Did you see/hear about FloudFlare offering an IPFS gateway? Will that affect/interface with Pirl Content MN?
````
Dubs: No, Pirl Marlin is a private IPFS network only to be used within the PIRL ecosystem.

```
clabmw24: how will you pay for the content masternodes? block rewards and pirltube users?
```
Dubs: I will temporarily keep the rewards inactive until we're sure Marlin is testing well and then adjust everything and start the rewards.

```
mk: I'd like to integrate the new contract for Marlin into the web wallet asap.
```
Dubs: Yep no problem.

Dubs also mentions that the responsibility for writing the new content masternode is on the community. There is already a bounty available for it on this very platform! Just see the Getting Started section. knowledgeable PIRL community members welcome with open arms.

```
blck: will you be able to limit max bandwidth used?
```
Dubs: No we won't limit it

He also mentioned that the setup for Marlin will be similar to the current setup.  It will be mainly handled by OneClick and Poseidon or the user will simply run the additional Marlin binary in addition to the premium binary in a manual setup scenario.

At this point Dubs announces he has a link for everyone.

https://storage.gra1.cloud.ovh.net/v1/AUTH_8f059abdcba74107a430604cf1c257bb/masternodes/content/pirl-content-v1-beta
https://storage.gra1.cloud.ovh.net/v1/AUTH_8f059abdcba74107a430604cf1c257bb/masternodes/marlin/marlin
https://storage.gra1.cloud.ovh.net/v1/AUTH_8f059abdcba74107a430604cf1c257bb/masternodes/premium/pirl-premium-v4-beta

To run simply...

`marlin init` followed by `marlin daemon`

Premium MNs will run the premium binary and marlin binary while content MNs will will the content binary and marlin binary.

```
Wracul: It's about 1 week to PirlApp. What more will be released as part of it?
```

Dubs: The goal of PirlApp is to publish an SDK allowing everyone to post apps on it.

He also mentioned that the soon to be released PirlTube will not allow pornography or nudity but PIRL may release a separate product for this market.

He again urges everyone who thinks he or she can help with any part of the project to contact him directly and express interest. This includes PirlTube moderators, marketing people, ProgPoW integrators and all others who want to work on a piece of PIRL.

Dubs says that he wants to only fork once and implement ProgPoW at the same time. Any development help to make this happen is appreciated from the community.

```
Phatblinkie: Have you had any other side conversations with the ProgPoW devs?
```
Dubs: Yes.  We don't want to implement as-is but improve parts it for our unique needs.


<iframe width="560" height="315" src="https://share.pirltube.com/content/video/0x741afdbc4f982a12a788ed5b674c7598e769d51e72bc9ebb4cebc81ac57e2876" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>


---
Author(s):

_[PrimateCrypto](https://twitter.com/PrimateCrypto)_

Contributor(s):

dptelecom
