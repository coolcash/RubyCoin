Rubycoin
========

A peer-to-peer digital currency, issued and managed without any central authority.
There is no government, company, or bank in charge of Rubycoin. As such, it is more resistant to wild inflation and corruption.

With Rubycoin, you can be your own bank on a decentralized network. Each user with a balance plays an important role in keeping the network fast, secure, and energy-efficient. Interest is automatically earned by every user that participates.


## Ubuntu / Debian

* Install dependencies

        $ sudo apt-get install build-essential libsodium-dev libssl-dev libdb++-dev libboost-all-dev make

* Clone from Github to get the source code:

        $ git clone https://github.com/rubycoinorg/rubycoin

* Now you can build rubycoind:

        $ cd rubycoin/src
        $ make -f makefile.unix


## OSX

* Install XCode with all the options checked. Download from https://developer.apple.com

* Clone from Github to get the source code:

        $ git clone https://github.com/rubycoinorg/rubycoin

* Download and install Homebrew from https://brew.sh

* Install dependencies

        $ brew install boost@1.57 berkeley-db4 libsodium openssl
        $ brew link boost@1.57 berkeley-db@4 libsodium openssl --force

* Optionally install qt (for Rubycoin-Qt)

        $ brew install qt@5.5 && brew link qt@5.5 --force

* Optionally install qrencode (and set USE_QRCODE=1)

        $ brew install qrencode && brew link qrencode --force

* Now you should be able to build rubycoind:

        $ cd rubycoin/src
        $ make -f makefile.osx

* Or rubycoin-qt:

        $ cd rubycoin
        $ qmake -o Makefile "USE_UPNP=-" BOOST_LIB_SUFFIX=-mt BDB_LIB_SUFFIX=-4.8
        $ make


## Getting Started

Run
  `./rubycoind -daemon` # Start the rubycoin daemon.

Run:
  `./rubycoind --help`  # List of command-line options.

Run
  `./rubycoind help` # When the daemon is running, get a list of RPC commands.
