# Editing Hostfile (optional)

If you are accessing the your web interfaces from another computer on your local network, (like if you have a server running that are you accessing from your desktop), you'll need to use a custom hostname so you can still use the great reverse proxy tooling included in this project.

In the normal configuration, we use the localhost domain, and add subdomains to that (e.g `sonarr.localhost`, `radarr.localhost`).
When connecting over LAN, localhost no longer points to the right server, and connecting like `sonarr.192.168.1.0` doesn't work.

To fix this, we're going to add a custom hostname in our hostfile.

## Add the domain to hostfile (linux)

> Note: This section is all performed on the computer you are accessing the server from, _not_ on the server

1. Open `/etc/hosts` (requires sudo permissions), e.g `sudo nano /etc/hosts`

2. Add a new line, and enter this:

```
server_ip_address_here  sonarr.fun radarr.fun bazarr.fun deluge.fun sabnzbd.fun organizr.fun jackett.fun traefik.fun ombi.fun hydra2.fun tautulli.fun lidarr.fun
```

Things to note:

- It is possible the above example becomes out of date. If you find you can't access a service, simply add another entry in the same pattern of `service_name.ending`
- `server_ip_address_here` is your server's local ip address, e.g `192.168.1.10`
- `service_name.fun` can use a domain ending (like `fun`), or use a domain (like `my_domain.com`). Some examples:
  - `sonarr.fun`
  - `sonarr.google.com`
  - `sonarr.media`
  - `sonarr.my.media`
- The domain ending can be whatever you want, even real urls, as it will override them in favor of your local mappings.

There are a few caveats here:

1. Your domain ending or domain name must have a valid ending, so `sonarr.asdfujh2wqesd` won't work. It must be a real domain ending.
2. In your `.env` file, you need to change the `LOCAL_DOMAIN=` option to whatever your domain ending/name is. For example, if I want to use `sonarr.fun`, I'd set that to `LOCAL_DOMAIN=fun`.
3. Whatever you choose must be consistent, so you can't do `sonarr.fun` and `radarr.media`, they have to use the same domain ending/name.

## Rest of the Guide

If you have to make these changes, whenever you see `service.localhost` in this guide, replace it with the mappings you setup, e.g `sonarr.localhost` -> `sonarr.fun`.
