# Traefik

By popular request here is the Traefik setup that I use for the NextCloud video.

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

