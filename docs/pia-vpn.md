# Setup PIA VPN

## Introduction

The goal here is to setup a general purpose vpn container to route certain traffic through. The most common use for the vpn is with your torrenting download client.

This guide uses PIA (PrivateInternetAccess) vpn to make it very easy to set up the vpn tunnel. Other vpns have to use other images, which aren't supported at this time.

This configuration is great, because it makes sure there is no leaky traffic outside of the vpn tunnel (solved by iptables), so if the vpn goes down all torrent traffic will be stopped and can't leak to your normal network.

## PIA Custom Setup

All you need to do to setup the vpn is to fill in the variables in the `.env` file. That's it! :D

## Other VPNs

If you are using another VPN it is possible to use that too. In that case, visit the [VPN with Open VPN](vpn-with-open-vpn.md) deprecated guide, and you will need to do custom setup.
