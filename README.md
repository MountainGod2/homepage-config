# Homepage Configs
  Personal collection of example config files for Homepage
 
  https://github.com/benphelps/homepage/
 
# Services.yaml
  There are two versions of `services.yaml` in this repository. The first is a sanitized version using standard keys.

  While the second, `services-env.yaml`, uses IP / key substitutions from environment variables used in the homepage container creation.

  Ex.
  
```
docker run
  -d
  --name=homepage
  -p 3000:3000/tcp
  -e HOMEPAGE_VAR_ROUTER_IP='192.168.0.1'
  -e HOMEPAGE_VAR_SERVER_IP='192.168.0.100'
  -e HOMEPAGE_VAR_PLEX_API_KEY='XXXXXXXXX'
  -e HOMEPAGE_VAR_TAUTULLI_API_KEY='XXXXXXXXX'
  -e HOMEPAGE_VAR_CLOUDFLARE_ACCOUNT_ID='XXXXXXXXX'
  -e HOMEPAGE_VAR_CLOUDFLARE_TUNNEL_ID='XXXXXXXXX'
  -e HOMEPAGE_VAR_CLOUDFLARE_TUNNEL_API_KEY='XXXXXXXXX'
  -e HOMEPAGE_VAR_TAILSCALE_DEVICE_ID='XXXXXXXXX'
  -e HOMEPAGE_VAR_TAILSCALE_API_KEY='tskey-api-XXXXXXXXX'
  -e HOMEPAGE_VAR_RADARR_API_KEY='XXXXXXXXX'
  ...
  -v /opt/homepage/config:/app/config:rw ghcr.io/benphelps/homepage
```

# Custom CSS Themes

  Also included is `customtheme.css` showing how to further customize the colours.
  
  The easiest methods to use are likely either via a subfilter module in Nginx (or similar), or with a browser extension such as Stylus.
 
  Ex.

```nginx
server {
# ...
    location / {
        proxy_set_header Accept-Encoding "";
        sub_filter
        '</head>'
        '<link rel="stylesheet" type="text/css" href="https://www.domain.com/customtheme.css">
        </head>';
        sub_filter_once on;

        proxy_pass http://host.ip:3000;
```

  or 

![homepage_stylus](https://github.com/MountainGod2/homepage_config/assets/88257202/531d0bc7-f6d4-4045-8f01-f3db13a4f874)



  # Screenshots

  With `fiveColumns: true` in settings.yaml
  
![homepage_dracula](https://github.com/MountainGod2/homepage_config/assets/88257202/d0157ecf-f4c7-4a57-aa8c-762b41e08591)

![homepage_ibracorp](https://github.com/MountainGod2/homepage_config/assets/88257202/4abcea11-22e8-46e0-bc33-56e6bec8af21)
