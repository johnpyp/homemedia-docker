# Initial Setup

## Install docker and docker-compose

1. See the [official instructions](https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/#install-docker-ce-1) to install Docker.

2. Then add yourself to the `docker` group:
   `sudo usermod -aG docker $USER`

3. Make sure it works fine:
   `docker run hello-world`

4. Also install docker-compose (see the [official instructions](https://docs.docker.com/compose/install/#install-compose)).

## Get docker-compose file

This tutorial will guide you through the process of configuring many different services for a homemedia server.

The included docker-compose file is your best option for having a seamless experience with little manual editing of the configuration files.

1. First, `git clone https://github.com/johnpyp/homemedia-docker` into a directory. This is where you will run the full setup from (note: this isn't the same as your media directory)

2. Enter the directory: `cd homemedia-docker`

3. Copy the `.env.example` file included in the directory to `.env`, e.g `cp .env.example .env`

## Setup environment variables

For each of these images, there is some unique coniguration that needs to be done. Instead of editing the docker-compose file to hardcode these values in, we'll instead put these values in a `.env` file. A `.env` file is a file for storing environment variables that can later be accessed in a general-purpose `docker-compose.yml` file, like the one in this repository.

Here is an example of what your `.env` file should look like; you should use values that fit for your own setup.

```bash
# Your timezone, https://en.wikipedia.org/wiki/List_of_tz_database_time_zones
TZ=America/New_York
# UNIX PUID and PGID, find with: id $USER
PUID=1000
PGID=1000
# The directory where data and configuration will be stored.
ROOT=/media/my_user/storage/homemedia

# PIA Information
PIA_USER=pia_username
PIA_PASS=pia_password
# This is your PIA region
PIA_REGION=US New York City

# Change this if accessing via LAN, you'll need to configure your hostfiles (coverered in the next section)
LOCAL_DOMAIN=localhost
# These options only need to be changed if you plan on using remote access + https
DOMAIN=my_domain.com
EMAIL=myemail@example.com
```

Things to notice:

- TZ is based on your [tz time zone](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones).
- The PUID and PGID are your user's ids. Find them with `id $USER`.
- The pia information are your credentials for [PrivateInternetAccess](https://privateinternetaccess.com), this is so the vpn can work safely.
- The last two options, `DOMAIN` and `EMAIL`, are only needed if you plan to use the remote + https configuration later on in this guide.
- This file should be in the same directory as your `docker-compose.yml` file so the values can be read in.

## Launch Services

Finally, in the directory, run `docker-compose up -d` to start all the services, with hopefully no errors if you entered good configuration.

```

```
