# Setup Organizr

[Organizr](https://github.com/causefx/Organizr) is a web UI to bring together all of your apps in one place. It allows you to setup "tabs" that will be loaded into one webpage. It will allow you to securely login to it and block access to anyone else. You can support multiple users, and guests as well.

## Docker Container

```yaml
organizr:
  container_name: organizr
  image: organizrtools/organizr-v2:latest
  restart: unless-stopped
  expose:
    - '80'
  environment:
    - PUID=${PUID} # default user id, defined in .env
    - PGID=${PGID} # default group id, defined in .env
  volumes:
    - ${ROOT}/config/organizr:/config
  labels:
    - 'traefik.backend=organizr'
    - 'traefik.local.frontend.rule=Host:organizr.localhost'
    - 'traefik.port=80'
    - 'traefik.enable=true'
```

## Configuration
