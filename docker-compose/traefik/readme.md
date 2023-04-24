# Traefik

By popular request here is the Traefik setup that I use for the NextCloud video.

## Config

Build a new server

1) fresh install of Ubuntu 22.04 server
2) `sudo apt update && sudo apt upgrade`
3) `sudo apt install vim`
4) install docker([How To Install and Use Docker on Ubuntu 22.04 | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-22-04)) & docker-compose([How To Install and Use Docker Compose on Ubuntu 22.04 | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-compose-on-ubuntu-22-04))
5) create traefik folder
6) write docker-compose.yml
7) create data folder
8) write config.yml
9) write traefik.yml
10) touch traefik.log
11) create letsencrypt folder
12) `docker network create -d bridge traefik-proxy`
13) `docker compose up --force-recreate -d`
14) check the traefik.log

## Few things:

This assumes you are using Cloudflare for your domains. If you are using something else look up how to do it [in the Traefik documentation.](https://doc.traefik.io/traefik/https/acme/#providers) For the most part you'll need to make these changes if you are using CLoudflare:

### docker-compose.yml

In the `environment` key enter a value for the `CF_API_EMAIL` (your Cloudflare E-mail address) and the `CF_API_KEY` (your Cloudflare api key). (Lines 21 and 22)

Then in the `labels` key enter a value for the `domains[0].main` and `domains[0].sans` (Lines 28 and 29). The main should be your bare domain and the sans should be the `*.` version of your domain.

### config.yml

In the `rule` key (Line 6) make sure to have your NextCloud domain in the value of this key in the form of:

```yaml
Host(`your.nextcloud.domain`)
```

Then in the `domains` `main` key (Line 12) add the same domain here.

Finally, make sure the `servers` `url` is set to the correct address. (Line 18)

