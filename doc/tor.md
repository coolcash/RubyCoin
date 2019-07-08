Tor Support
=========

Rubycoin can be run as a hidden service.


## Ubuntu / Debian

* Install Tor

        $ sudo apt-get install tor

* Prepare folder

        $ mkdir /var/lib/tor/hidden_service
        $ chmod 700 /var/lib/tor/hidden_service
        $ chown debian-tor:debian-tor /var/lib/tor/hidden_service

* Edit /etc/tor/torrc

        $ sed -i '0,/#HiddenServiceDir/s//HiddenServiceDir/' /etc/tor/torrc
        $ sed -i '0,/#HiddenServicePort 80 127.0.0.1:80/s//HiddenServicePort 5937 127.0.0.1:5937/' /etc/tor/torrc

* Restart service

        $ service tor restart

* Get onion address (for the next step)

        $ cat /var/lib/tor/hidden_service/hostname

* Edit config

        $ sh -c "echo 'externalip=YOUR_TOR_HOSTNAME.onion'" >> ~/.rubycoin_v2/rubycoin.conf
        $ sh -c "echo 'listen=1\ndiscover=1\ntor=127.0.0.1:9050'" >> ~/.rubycoin_v2/rubycoin.conf

* Restart rubycoind

        $ ./rubycoind stop
        $ ./rubycoind -daemon

* Verify syncing

        $ ./rubycoind getinfo
        "blocks" : 12345
        "connections" : 8
        "ip" : "YOUR_TOR_HOSTNAME.onion"


## Privacy

When **externalip** is specified, no attempt is made to discover local IPv4 or IPv6 addresses. If you want to run a dual setup, reachable from both Tor and the clearnet, you will need to either pass your other addresses using **externalip**, or enable **discover**. All addresses of a dual setup may be easily linkable using traffic analysis.