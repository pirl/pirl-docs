# [Windows] How to setup Github + GitKraken and start contribute

Hey fellow, if you seek to contribute with pirl docs, the following guides should be usefull for people who didn't use github.

In this guide, you will see how to create an account, fork the main repo and clone it to start to contribute


## Requirements

Firstly, go to [github](https://github.com) and create an account if you doesn't have one yet

Then I recommand you to use GitKraken (free for open source, it's our case), you can download it on [https://www.gitkraken.com/](https://www.gitkraken.com/)

When it's done, connect with your github account.
![GitKrakenSignIn](media/gitKrakenSignIn.png)
![GitKrakenSetupProfile](media/gitKrakenSetupProfile.png)

You'll need a text editor, you can use any one you want. 

For instance I use notepad++ : [https://notepad-plus-plus.org/downloads/](https://notepad-plus-plus.org/downloads/)

You have now the requirements needed to setup things !

## Setup

Go to the official depot : [https://github.com/pirl/pirl-docs](https://github.com/pirl/pirl-docs)

Then click on fork
[<img src="media/githubFork.png"/>](media/githubFork.png)

You can retreive the fork under `Your repositories`
![YourRepositories](media/yourRepositories.png)

Then you can access it by clicking on the name
![SelectRepo](media/selectRepo.png)

Now click on `Code` then copy the URL
[<img src="media/getUrlForClone.png"/>](media/getUrlForClone.png)

Go on gitkraken then click on `clone a repo`
![CloneWithGitKraken](media/cloneRepoGitKraken.png)

Choose your path then paste your previously copied URL
![SetupClone](media/cloneSettings.png)

You can now open the cloned repo
![OpenRepo](media/openRepo.png)

You will need to download `mdbook` for windows at [https://github.com/rust-lang/mdBook/releases](https://github.com/rust-lang/mdBook/releases)
![mdbook](media/mdbook.png)

Extract it next to your `pirl-docs` folder
![mdbookPlace](media/placingMdbook.JPG)

Then go on `File` -> `Preferences...`

![settingGitKraken](media/settingGitKraken.png)

Then select `PowerShell` under `Default Terminal`
![terminalGitKraken](media/terminalGitKraken.png)

You can exit Preferences.

You all now set to start contribute ! 
See the next [guide](write_your_first_doc.md) learn to how to write your first docs

<p align=right> Written by WeHaveCookie </p>