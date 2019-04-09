# Setup HTTPS Reverse Proxy (optional)

In the base version of our docker-compose file, a "reverse proxy" is used so that instead of typing some thing like `localhost:8989` you get to type the easy-to-remember `sonarr.localhost`.

This reverse proxy has a lot of potential in what it can do past the base version, which is what is expanded upon here.

This section goes over adding three key features to the base reverse proxy configuration:

- Portforward your network and access it via a domain, e.g `sonarr.my_domain.com`
- Secure the connection with free https, e.g `https://sonarr.my_domain.com`
- Authentication with Organizr

## Requirements

- A domain
- Able to portforward/access your router configuration

## Change to New Preset

Currently, you are probably using the `docker-compose.yml` file in the `base` configuration. You'll want to go into the `https` directory instead.

The configuration will be completely usable with the `base` configuration, so you can copy over your current `.env` file into the `https` directory as well.

You'll need to add a few more fields to your .env file, and these are also outlined in the `.env.example` file in the https directory.

```bash
# ... previous configuration
DOMAIN=my_domain.com
EMAIL=myemail@example.com
```

- The domain is your personal domain that you need to be able to point at your local network after you portforward it.

## Configuration

To get https and remote access working, you'll need to:

1. Portforward ports 80 and 443 from your computer, or open them on a server that you are running this on. Port forwarding is somewhat advanced, and it requires you to edit your router configuration. There are some great tutorials on doing this, and it _should_ be relatively straight forward.

2. Point your domain at your ip and these ports. First, you'll want to find you public ip (https://www.whatismyip.com). In your domain's DNS configuration, you'll need to make an `A` record for every service you want to be able to access remotely. This a record will be coming from a subdomain with the name of the service and pointing at your public ip address. For example, you would create an A record from deluge.my_domain.com to 123.12.34.56.

These are the service names you'll need to make subdomain A records for that are covered in this tutorial:

- deluge
- nzbget
- jackett
- sonarr
- radarr
- bazarr
- organizr
- traefik

Once these two steps are done, you should be able to run the containers with `docker-compose up -d` and your services will now be setup. To login remotely, you'll need to login to organizr at `https://organizr.my_domain.com`, then you'll be able to access all of your other services through organizr or at their subdomains, e.g `https://sonarr.my_domain.com`

If you don't login to organizr, you'll get a 401 error. Don't be alarmed, this is so unauthenticated users can't manipulate your services.

They will also be available at `service_name.localhost` without needing to login and without https, so you can access them directly on your local network as you did in the base tutorial.

Additionally, the Web Monitor UI for Traefik will be available at `traefik.localhost`.

### Basic Authentication - Not Recommended

**This is not recommended because there is no persistance after browser restarts, you have to authenticate to each service individually, and you'll still have to authenticate within organizr even after you authenticate into organizr itself**

If you don't want to use the included Organizr authentication, which makes it simple and easy to authenticate to all of your services remotely, you can use basic authentication instead.

You'll want to create two more environment variables in your `.env` configuration called `USERNAME` and `PASSWORD`. Fill these with either side of a username:password_hash combination you can generate [here](http://www.htaccesstools.com/htpasswd-generator/)

Then, in your `docker-compose.yml`, you'll need to uncomment the line about basic authentication, and comment out the line above it, in most of the services that have it present. This should be all you need for basic authentication.
