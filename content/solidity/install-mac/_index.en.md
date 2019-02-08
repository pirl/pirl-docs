---
title: Pirl Node - Installing on Mac
weight: 9
pre: "<b>9. </b>"
chapter: true
---
## Building from source

### Building Pirl (command line client)

Clone the repository to a directory of your choosing:

```shell
git clone https://github.com/pirl/pirl/
```

Building `pirl` requires the Go compiler:

```shell
brew install go
```

Finally, build the `Pirl` program using the following command.
```shell
cd pirl
make pirl
```

If you see some errors related to header files of Mac OS system library, install XCode Command Line Tools, and try again.

```shell
xcode-select --install
```

You can now run `build/bin/Pirl` to start your node.



---
Author(s):  

@Fawkes

Contributor(s):  

@Dptelecom
