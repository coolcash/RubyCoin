Staking on a Raspberry Pi
===================================

The Raspberry Pi is a series of small single-board computers intended to promote the teaching of basic computer science in schools and developing countries. Rubycoin can stake on these devices.


## Raspbian

* Increase swap memory

        $ sudo sed -i 's/CONF_SWAPSIZE=100/CONF_SWAPSIZE=1024/g' /etc/dphys-swapfile

* Restart service

        $ sudo /etc/init.d/dphys-swapfile stop
        $ sudo /etc/init.d/dphys-swapfile start

* Install dependencies

        $ sudo apt update
        $ sudo apt install git build-essential libdb++-dev libboost-all-dev libsodium-dev libssl1.0-dev make

* Set timezone and locale under localization options

        $ sudo raspi-config

* Compile Rubycoin

        $ git clone https://github.com/rubycoinorg/rubycoin
        $ cd rubycoin/src
        $ make -f makefile.unix

* Edit config

        $ mkdir ~/.rubycoin_v2
        $ sh -c "echo 'rpcuser=rubycoinrpc'" >> ~/.rubycoin_v2/rubycoin.conf
        $ sh -c "echo 'rpcpassword=YOUR_RPC_PASSWORD'" >> ~/.rubycoin_v2/rubycoin.conf

* Start rubycoind

        $ ./rubycoind -daemon

* Verify syncing

        $ ./rubycoind getinfo
        "blocks" : 12345
        "connections" : 8

* Encrypt wallet

        $ ./rubycoind encryptwallet YOUR_SUPER_SECURE_PASSWORD

* Decrypt for staking only

        $ ./rubycoind walletpassphrase YOUR_SUPER_SECURE_PASSWORD 31557600 true

* Get an address to fund for staking

        $ ./rubycoind getnewaddress


## Swap memory

After compiling, swap memory should be decreased back to the default value.

* Decrease swap memory

        $ sudo sed -i 's/CONF_SWAPSIZE=1024/CONF_SWAPSIZE=100/g' /etc/dphys-swapfile

* Restart service

        $ sudo /etc/init.d/dphys-swapfile stop
        $ sudo /etc/init.d/dphys-swapfile start


## External drive

Compile time can be improved by using an external drive.

* Mount drive

        $ mkdir ~/.rubycoin_v2
        $ sudo mount /dev/sdXY ~/.rubycoin_v2


## Desktop wallet

A graphical interface for the Rubycoin wallet is optionally available.

* Install dependencies

        $ sudo apt install qt5-default qt5-qmake qtbase5-dev-tools qttools5-dev-tools

* Compile Rubycoin

        $ cd rubycoin
        $ qmake
        $ make

## Troubleshooting

If you encounter:

        E: You don't have enough free space in /var/cache/apt/archives/.

Remove unnecessary installation files:

        $ sudo apt clean

