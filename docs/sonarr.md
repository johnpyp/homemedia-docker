# Setup Sonarr

**_Note: This configuration section uses the old version of Sonarr, rather than the new v3 version. This section should be updated soon™. Most of the princples apply, but the UI will look different than in the images._**

## Configuration

Sonarr should be available on `sonarr.localhost`. Go straight to the `Settings` tab, then the `Media Management` tab.

![Sonarr settings](img/sonarr_media_management.png)

Make sure Advanced options are enabled, and make these changes:

- Enable: Rename Episodes
- Standard Episode Format: `{Series Title} - S{season:00}E{episode:00} - {Episode Title} {Quality Title} {MediaInfo Full}-{Release Group}`
- Daily Episode Format: `{Series Title} - {Air-Date} - {Episode Title} {Quality Title} {MediaInfo Full}-{Release Group}`
- Anime Episode Format: `{Series Title} - S{season:00}E{episode:00} - {Episode Title} {Quality Title} {MediaInfo Full}-{Release Group}`
- Enable: Import Extra Files
- Import Extra Files: `srt,nfo`

In `profiles` you can set new quality profiles, default ones are fairly good. There is an important option at the bottom of the page: do you want to give priority to Usenet or Torrents for downloading episodes? I'm keeping the default Usenet first.

![Sonarr Indexers Newznab](img/sonarr_indexers_newznab.png)

> Note: This section is for usenet, if you aren't using usenet you can skip this.

`Indexers` is the important tab: that's where Sonarr will grab information about released episodes. Nowadays a lot of Usenet indexers are relying on Newznab protocol: fill-in the URL and API key you are using. You can find some indexers on this [subreddit wiki](https://www.reddit.com/r/usenet/wiki/indexers). It's nice to use several ones since there are quite volatile. You can find suggestions on Sonarr Newznab presets. Some of these indexers provide free accounts with a limited number of API calls, you'll have to pay to get more. Usenet-crawler is a good free indexer option.

![Jackett indexers](img/jackett_indexers.png)

![Sonarr torznab add](img/sonarr_indexers_torznab.png)

> Note: This section is for torrents, if you aren't using torrents you can skip this.

For torrents indexers, I activate Torznab custom indexers that point to my local Jackett service. This allows searches across all torrent indexers configured in Jackett. You have to configure them one by one though.

Get torrent indexers Jackett proxy URLs by clicking `Copy Torznab Feed` in Jackett Web UI. Use the global Jackett API key as authentication.

**_Note: You must change the host url to `jackett:9117` as shown in the image above._**

`Download Clients` tab is where we'll configure links with our two download clients: NZBGet and Deluge.
There are existing presets for these 2 that we'll fill with the proper configuration.

NZBGet configuration:
![Sonarr NZBGet configuration](img/sonarr_nzbget.png)

Deluge configuration:
![Sonarr Deluge configuration](img/sonarr_deluge.png)

Enable `Advanced Settings`, and tick `Remove` in the Completed Download Handling section. This tells Sonarr to remove torrents from deluge once processed.

In `Connect` tab, we'll configure Sonarr to send notifications to Plex when a new episode is ready:
![Sonarr Plex configuration](img/sonarr_plex.png)

## Give it a try

Let's add a series !

![Adding a serie](img/sonarr_add.png)

_Note: You may need to `chown -R $USER:$USER /path/to/root/directory` so Sonarr and the rest of the apps have the proper permissions to modify and move around files._

Enter the series name, then you can choose a few things:

- Monitor: what episodes do you want to mark as monitored? All future episodes, all episodes from all seasons, only latest seasons, nothing? Monitored episodes are the episodes Sonarr will download automatically.
- Profile: quality profile of the episodes you want (HD-1080p is the most popular I guess).

You can then either add the serie to the library (monitored episode research will start asynchronously), or add and force the search.

![Season 1 in Sonarr](img/sonarr_season1.png)

Wait a few seconds, then you should see that Sonarr started doing its job. Here it grabed files from my Usenet indexers and sent the download to NZBGet automatically.

![Download in Progress in NZBGet](img/nzbget_download.png)

You can also do a manual search for each episode, or trigger an automatic search.

When download is over, you can head over to Plex and see that the episode appeared correctly, with all metadata and subtitles grabbed automatically. Applause !

![Episode landed in Plex](img/mindhunter_plex.png)
