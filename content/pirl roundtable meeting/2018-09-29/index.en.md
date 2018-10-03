---
title: PIRL Meeting Notes - 2018/09/29
weight: 5
disableToc: true
---

## TL;DR ##
PirlTube is released today for testing! You can use PirlApp to access it once it finishes compiling!
Oh wait, there it is! PirlApp and PirlTube are out https://drive.google.com/drive/folders/13CUHTDr3bB0zBeWb0ebHEJ0H8TY8evR4

> This link will expire after the beta testing. For all current releases see the official http://www.pirl.io

## 2018/09/29 - PirlTube and PirlApp

Fawkes says that the Pirl team is running final tests and checking everything for the new releases. He says Dubs and Is are currently working on finalizing and building PirlApp, which will be released later today! 

```
daxm: 1-click install is really pushed as "the way".  Will there be a time that is the ONLY way to install a PIRL MN?
```
Fawkes: OneClick will not be the only way to install masternodes. The Pirl team is trying to make everything as decentralized as possible and having an independent servers goes toward that.

He also mentions how he's happy to see the round table meeting grow since its inception.

```
Don: what was the problem that all MNs had to change the tokens?
```
Fawkes: Unfortunately we will need masterdubs to answer this question later.

Masterdubs jumps in!

Dubs: That was a misstep with the 2 masternode types. It was not expected. Sorry, shit happens and MN owners have been compensated for the unfortunate outage.

```
MacMiner: any plans to bring the PIRL App to IOS and Android and if so any date you can give us?
```
Fawkes: First the desktop app will be finished and polished and later PirlApp will be put on as many platforms as possible.

```
Test.Object. 001: I would like to do an interview with Masterdub if there could be a possibility and publish it as an article. Hello mr. Masterdub!
```
Masterdubs: We will do it after I free up with current projects which are taking all of my time.

```
daxm: For future (non-beta) releases, how will it be conveyed to the MN owners that they need to update?  (Not everyone can camp in Discord and read all the Pinned messages.)  Just wondering how we all will keep up-to-date.
```
Masterdubs: SMS notifications will be implemented and other ways as well to notify MN owners of any outages.

Fawkes jokes that the sooner the meeting ends we will be able to start focusing on finalizing the release!

```
Don: can we get a rough overview of the new MNs planned prices for storage space and technical implementation just an overview of what is planned. It can also change something but that we know the direction where it go
```
Fawkes: If you want to ensure a good operation of your Masternode, it's good to upgrade to over 4GB RAM.
Masterdubs: The more storage you have the better.  The more storage you have, the more bandwidth you'll be paid for possibly.

Dubs mentions that we want MNs to be beefy in order to feed the needs of the network.

The discussion continues about OVH and how their crummy practices are not OK. They promise 4GB of RAM but provide less than that, which makes V5 of the masternode software unable to run. Community action is discussed to address this shortcoming.

```
daxm: I have a "different" question:  What are the dots supposed to represent on https://poseidon.pirl.io/?  I ask because my MN location is certainly not showing up (if that is what is being presented).
```
Dubs: The issue is scaling. Once scaled the issue will be resolved and all nodes will be listed.

```
PrimateCrypto: Can we discuss Content MN & PirlTube costs rewards? How much of the total 3 Pirl block reward will content MNs get? How much for content?
Will PirlTube creators be paying to upload videos in addition to the small gas fees?
Will there be any fees for watching videos?
```
The block rewards will be split with 2 going to premium .5 going to content and .5 going to storage (to be released). After that we will distribute advertisement. Every part of ecosystem gets its share but most of the revenue will go to the publisher. Also, the owners of masternodes will be rewarded too.

Fawkes: Also, in the next update, we will have possibility for content creators to contribute to "pay to watch". This will be good for guys who are able to create guides, lessons and online teaching and such. So people will pay to watch those videos and we will create over time some way how to reward these creators.

```
NewbieDriver: I would like to know which audio and video codec will be used for PirlTube?
```
Dubs: You will have your respond when you will see running PirlTube.

```
PrimateCrypto: What will be a maximal size of uploaded video?
```
Dubs: The size will be set for 1 Gb for now.

```
inmortem: Will PT allow private videos as YouTube does?
```
Fawkes: Yes, this is really standard stuff. If you post any copy-right material this is entirely your problem but platform will be forced to delete such content. We will use simple reports to specialized team who will be solving such issues. more thing about private video will be add in next versions, but basically everything will go trough some kind of moderation, even if it is a private video. There will be no options for private video in first version. Next thing witch will not be in the first version but will be definitively in next version is a life stream. And to be honest, decentralized live-streaming is really something new.

Dubs: Yes, there will be an very easy options to report a bad video.

```
Don: Will it be easy to copy channels from YT to PT over YT API?
```
Dubs: Yeah, we will be able to copy paste from YouTube channel into PirlTube channel. You will be able to import when the product will be out of beta testing phase.

```
inmortem: Will PT prevent offline downloading of content in anyway?  For example to block YouTube downloaders?
```
Fawkes: right now there is no possibility to download video from the application and also there is no possibility to use something like youtube downloader.
```
daxm: Do we have Docs on how to configure/modify Marlin?  (I'm looking at the PirlDocs menu right now and I don't see anything there.)
```
Fawkes: No, not yet. It were rough 4 months for us. it will be preconfigured at this stage. we will build documentation as we follow. We are running behind documentations.
That's we rely on PrimateCrypto who is helping us with documentations. Everyone is welcome to do it. We will not do it officially. Commands for Marlin are pretty much the same as for RpFs. We will have some customization about preserving integrity.
Basically every help is welcome and will be rewarded. We are com based project so we want
to have community engagement and involve more people into the project.
We cab do the documentation by ourselves but we want to focused on next tasks.
But more and more stuff is incoming. We will have marketplace, mobile version of Poseidon
,the PIRL storage, the updates for PirlTube, new version of Poseidon and much more hard work and more time consuming task are in front of us.

We have a lot of new stuff. Now we only need to work hard and deliver this to you :)

```
mk: any general estimate of when to expect storage nodes?
```
Fawkes: All storage nodes events are planed for next year.  Storage nodes are implementation of Casandra but we need to set them from the scratch. It will be something like Google drive but decentralized. There will be possibility to store private files and makes public folders and share them and so on.

```
Test.Object. 001 something like STORJ?
```
Dubs: We are not really aware of how STORJ works so I cant give you any straight answer for that.

```
inmortem: Will comments / discussion on a video be stored on Content Node.  Who moderates comments / discussion?  Can it be turned off...
```
Fawkes: We Don't have comments or discussions in the first version of PirlTube.
We want to be independent on the servers so that no failure can occur.

```
mk: do you have any awesome videos preloaded on PirlTube that we can see?
```
Fawkes: Guys, you will be the ones who will be uploading our first videos.
Or Fat rabbit can upload a videos for us. Who wants FatRabbit to upload videos for us write #FaRrabbit

30 People write #FatRabbit :)

Bye bye guys.






Author(s):
_[PrimateCrypto](https://twitter.com/PrimateCrypto)_

Contributor(s):
_[Test.Object. 001](https://twitter.com/MickeyMaler)_
