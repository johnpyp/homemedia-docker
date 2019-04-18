# Setup Sabnzbd

[Sabnzbd](https://sabnzbd.org/) is an open-source usenet downloader. This will be used to download from our usenet backend, and integrate with Sonarr/Radarr.

## Configuration and usage

The Web UI is available at `localhost:8081`. After we configure this, you can access it at `sabnzbd.localhost`.

First, choose your language and click Start Wizard.

Since NZBGet stays on my local network, I choose to disable passwords (`Settings/Security/ControlPassword` set to empty).

The important thing to configure is the url and credentials of your newsgroups server (`Settings/News-servers`). I have a Frugal Usenet account at the moment, I set it up with TLS encryption enabled.

Default configuration suits me well, but don't hesitate to have a look at the `Paths` configuration.

You can manually add .nzb files to download, but the goal is of course to have Sonarr and Radarr take care of it automatically.
