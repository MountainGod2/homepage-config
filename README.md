# Homepage Configs

  Personal collection of example config files for [benphelps/homepage](https://github.com/benphelps/homepage/)
  
# Services.yaml
  There are two versions of the services configuration file in this repository.

  The first is a sanitized version using standard keys:
  
  [`services.yaml`](https://github.com/MountainGod2/homepage-config/blob/main/services.yaml)

  While the second uses IP / key substitutions from environment variables used in the homepage container creation:
  
  [`services-env.yaml`](https://github.com/MountainGod2/homepage-config/blob/main/services-env.yaml)

  Example docker run command using standard config files:
```yaml
docker run \
  -d \
  --name='homepage' \
  --net='dsn' \ # user-defined bridge network to refer to containers by hostname instead of IP
  -e TZ="America/Denver" \
  -v '/mnt/':'/mnt':'ro' \ # read-only volume mount
  -v '/mnt/user/appdata/homepage/config':'/app/config':'rw' \
  -v '/mnt/user/appdata/homepage/images/':'/app/public/images':'rw' \
  -v '/mnt/user/appdata/homepage/icons/':'/app/public/icons':'rw' \
  -p '3000:3000/tcp' \
'ghcr.io/benphelps/homepage'
```

  Example docker run command using environment label substitutions:
```yaml
docker run \
  -d \
  --name='homepage' \
  --net='dsn' \ # user-defined bridge network to refer to containers by hostname instead of IP
  -e TZ="America/Denver" \
  -e 'HOMEPAGE_VAR_ROUTER_IP'='192.168.0.1' \
  -e 'HOMEPAGE_VAR_SERVER_IP'='192.168.0.100' \
  -e 'HOMEPAGE_VAR_CLOUDFLARE_ACCOUNT_ID'='XXXXX' \
  -e 'HOMEPAGE_VAR_CLOUDFLARE_TUNNEL_ID'='XXXXX' \
  -e 'HOMEPAGE_VAR_CLOUDFLARE_TUNNEL_API_KEY'='XXXXX' \
  -e 'HOMEPAGE_VAR_TAILSCALE_DEVICE_ID'='XXXXX' \
  -e 'HOMEPAGE_VAR_TAILSCALE_API_KEY'='tskey-api-XXXXX' \
  -e 'HOMEPAGE_VAR_OVERSEERR_API_KEY'='XXXXX' \
  -e 'HOMEPAGE_VAR_QBITTORRENT_UN'='XXXXX' \
  -e 'HOMEPAGE_VAR_QBITTORRENT_PW'='XXXXX' \
  -e 'HOMEPAGE_VAR_SABNZBD_API_KEY'='XXXXX' \
  -e 'HOMEPAGE_VAR_PLEX_API_KEY'='XXXXX' \
  -e 'HOMEPAGE_VAR_TAUTULLI_API_KEY'='XXXXX' \
  -e 'HOMEPAGE_VAR_RADARR_API_KEY'='XXXXX' \
  -e 'HOMEPAGE_VAR_RADARR4K_API_KEY'='XXXXX' \
  -e 'HOMEPAGE_VAR_SONARR_API_KEY'='XXXXX' \
  -e 'HOMEPAGE_VAR_BAZARR_API_KEY'='XXXXX' \
  -e 'HOMEPAGE_VAR_PROWLARR_API_KEY'='XXXXX' \
  -e 'HOMEPAGE_VAR_OPNSENSE_UN'='XXXXX' \
  -e 'HOMEPAGE_VAR_OPNSENSE_PW'='XXXXX' \
  -e 'HOMEPAGE_VAR_ADGUARD_UN'='XXXXX' \
  -e 'HOMEPAGE_VAR_ADGUARD_PW'='XXXXX' \
  -e 'HOMEPAGE_VAR_HOMEASSISTANT_LLAT'='XXXXX' \
  -v '/mnt/':'/mnt':'ro' \ # read-only volume mount
  -v '/mnt/user/appdata/homepage/config':'/app/config':'rw' \
  -v '/mnt/user/appdata/homepage/images/':'/app/public/images':'rw' \
  -v '/mnt/user/appdata/homepage/icons/':'/app/public/icons':'rw' \
  -p '3000:3000/tcp' \
'ghcr.io/benphelps/homepage'
```

# Custom CSS Themes

  Also included is [`customtheme.css`](https://github.com/MountainGod2/homepage-config/blob/main/customtheme.css) showing how to customize the colours further.
  
  The easiest method is likely either via a browser extension such as Stylus, or by using a subfilter module in Nginx (or similar).

  Ex.

![homepage_stylus](https://github.com/MountainGod2/homepage_config/assets/88257202/531d0bc7-f6d4-4045-8f01-f3db13a4f874)

  or 

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




  # Screenshots

  With `fiveColumns: true` in settings.yaml
  
![homepage_dracula](https://github.com/MountainGod2/homepage_config/assets/88257202/d0157ecf-f4c7-4a57-aa8c-762b41e08591)

![homepage_ibracorp](https://github.com/MountainGod2/homepage_config/assets/88257202/4abcea11-22e8-46e0-bc33-56e6bec8af21)
