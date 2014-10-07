# BitHammer

#### The last conversation you'll ever have about BitTorrent using up the network.

    NOTE: This program is aggressive.  Before using it, you should get permission from the owner of any network you are using.  You assume all responsibility for it's use.

BitTorrent is ok.  Using BitTorrent on public wifi is not.  BitTorrent aggressively soaks up bandwidth and connections, rendering other programs useless and users frustrated.

http://askubuntu.com/questions/16680/using-a-bittorrent-client-slows-down-internet-connection

After a year of traveling, struggling with broken wifi spots, and talking with frustrated helpless non-technical people who owned/managed them, I wrote this script to help network users and owners.

This program listens for BitTorrent clients on the network, adds their IP's to a ban list, then bans them from the network for as long as the program is running.

## To run on Linux:

Install `python` and `scapy`:

    sudo apt-get install python python-scapy

Run the program:

    git clone <this repository>
    cd bithammer
    sudo python ./bithammer

The `scapy` library requires `root` priviledges.

## To run on Windows or MacOS

Pull requests welcome.  This may help:

    http://www.secdev.org/projects/scapy/doc/installation.html#platform-specific-instructions

## How does it work?

The program listens for BitTorrent users advertising themselves via LPD:  

    http://en.wikipedia.org/wiki/Local_Peer_Discovery

The program then bans those users from the network via ARP Cache poisoning:

    http://danmcinerney.org/arp-poisoning-with-python-2/

Network Traffic to/from the banned computer is redirected to your computer, which then ignores it.  The program continues to poison the ARP cache for any computers advertising LDP.

## Is this legal?

I am not a lawyer.  Get permission before using it on someone else's network.

## It's not working

There are a variety of reasons it may not work.  

 - You're bandwidth problem may unrelated to BitTorrent
 - BitTorrent clients may not be advertising with LDP
 - The wifi access point may isolate users from each other
 - Something else

## I think I'm getting banned!  Are you anti-bittorrent, pro-hitler, and anti-puppies?

Climate change, ocean collapse, and crappy wifi are all tradgedies of the commons.

http://en.wikipedia.org/wiki/Tragedy_of_the_commons

It's not personal.  It's just that you're breaking it for everyone else.

## Can I permanently ban someone?

Yes, log into your router and add the mac address to the ban list:

http://blog.dlink.com/how-to-block-devices-from-your-home-network/

(This is specific to your router and you'll need the router admin password.)

The mac address has the :'s in it:

    Starting BitHammer.
      = 192.168.1.7 -> 00:11:22:33:44:55, new ban added

