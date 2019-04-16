# Setup a VPN Container

## Introduction

_Section Needs work_

The goal here is to have an OpenVPN Client container running and always connected. We'll make Deluge incoming and outgoing traffic go through this OpenVPN container.

This must come up with some safety features:

1. VPN connection should be restarted if not responsive
1. Traffic should be allowed through the VPN tunnel _only_, no leaky outgoing connection if the VPN is down
1. Deluge Web UI should still be reachable from the local network

Lucky me, someone already [set that up quite nicely](https://github.com/dperson/openvpn-client).

Point 1 is resolved through the OpenVPN configuration (`ping-restart` set to 120 sec by default).
Point 2 is resolved through [iptables rules](https://github.com/dperson/openvpn-client/blob/master/openvpn.sh#L52-L87)
Point 3 is also resolved through [iptables rules](https://github.com/dperson/openvpn-client/blob/master/openvpn.sh#L104)

Configuration is explained on the [project page](https://github.com/dperson/openvpn-client), you can follow it.
However it is not that easy depending on your VPN server settings.
I'm using a privateinternetaccess.com VPN, so here is how I set it up.

## PIA Custom Setup

_Note_: this section only applies for [PIA](https://privateinternetaccess.com) accounts.

The VPN Setup in this guide expects you to use PIA, which is my highly preferred choice for VPN, as it is cheap, very fast, and has good support.

The setup for this vpn is very easy, just fill out the environment variables in your .env file (maybe you already did it in the Initial Setup part). This is all!

## Other VPNs

In this guide, we are using a custom PIA docker container to make things easier, however if you are using another VPN it is possible to use that too. In that case, visit the [VPN with Open VPN](vpn-with-open-vpn.md) deprecated guide.
