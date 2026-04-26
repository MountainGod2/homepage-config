# Homepage Config

My personal configuration files for [gethomepage/homepage](https://github.com/gethomepage/homepage/).

## Setup

### Prerequisites

- Docker and a user-defined Docker network (`docker network create my-network`)
- A [docker-socket-proxy](https://github.com/Tecnativa/docker-socket-proxy) container on the same network (referenced as `dockersocket:2375` in `docker.yaml`)
- A `.env.homepage` file with the required environment variables

### Run

```bash
docker run \
  -d \
  --name homepage \
  --net my-network \
  --env-file /path/to/.env.homepage \
  -e TZ="America/Edmonton" \
  -p 3000:3000 \
  -v /path/to/config:/app/config:rw \
  -v /path/to/icons:/app/icons:rw \
  -v /path/to/images:/app/images:rw \
  -v /mnt:/mnt:ro \
  ghcr.io/gethomepage/homepage:latest
```

The `/mnt` bind mount is required for the disk widgets in `widgets.yaml` to read Unraid array and cache disk usage.

### Environment Variables

`{{HOMEPAGE_VAR_*}}` placeholders are substituted at container buildtime from enviroment variables.

| Variable | Used by |
|---|---|
| `HOMEPAGE_VAR_DOMAIN_NAME` | All service URLs |
| `HOMEPAGE_VAR_ROUTER_IP` | OPNSense, Tailscale ping, AdGuard |
| `HOMEPAGE_VAR_UNRAID_API_KEY` | Unraid widget |
| `HOMEPAGE_VAR_URBACKUP_USERNAME` | UrBackup widget |
| `HOMEPAGE_VAR_URBACKUP_PASSWORD` | UrBackup widget |
| `HOMEPAGE_VAR_TAILSCALE_DEVICE_ID` | Tailscale widget |
| `HOMEPAGE_VAR_TAILSCALE_API_KEY` | Tailscale widget |
| `HOMEPAGE_VAR_RADARR_API_KEY` | Radarr widget |
| `HOMEPAGE_VAR_SONARR_API_KEY` | Sonarr widget |
| `HOMEPAGE_VAR_BAZARR_API_KEY` | Bazarr widget |
| `HOMEPAGE_VAR_OVERSEERR_API_KEY` | Overseerr widget |
| `HOMEPAGE_VAR_OPNSENSE_KEY` | OPNSense widget |
| `HOMEPAGE_VAR_OPNSENSE_SECRET` | OPNSense widget |
| `HOMEPAGE_VAR_PROWLARR_API_KEY` | Prowlarr widget |
| `HOMEPAGE_VAR_SABNZBD_API_KEY` | SABnzbd widget |
| `HOMEPAGE_VAR_QBITTORRENT_USERNAME` | qBittorrent widget |
| `HOMEPAGE_VAR_QBITTORRENT_PASSWORD` | qBittorrent widget |
| `HOMEPAGE_VAR_CROWDSEC_USERNAME` | CrowdSec widget |
| `HOMEPAGE_VAR_CROWDSEC_PASSWORD` | CrowdSec widget |
| `HOMEPAGE_VAR_PLEX_API_TOKEN` | Plex widget |
| `HOMEPAGE_VAR_TAUTULLI_API_KEY` | Tautulli widget |
| `HOMEPAGE_VAR_CLOUDFLARE_ACCOUNT_ID` | Cloudflare tunnel widget |
| `HOMEPAGE_VAR_CLOUDFLARE_TUNNEL_ID` | Cloudflare tunnel widget |
| `HOMEPAGE_VAR_CLOUDFLARE_TUNNEL_API_KEY` | Cloudflare tunnel widget |
| `HOMEPAGE_VAR_ADGUARD_USERNAME` | AdGuard widget |
| `HOMEPAGE_VAR_ADGUARD_PASSWORD` | AdGuard widget |
| `HOMEPAGE_VAR_HOMEASSISTANT_LLAT` | Home Assistant widget |

---

## Theme

`config/custom.css` contains a Dracula theme based on [homepage-dracula](https://github.com/Jas-SinghFSU/homepage-dracula).
`settings.yaml` must have `color: gray` uncommented, or colour must be manually chosen, for it to apply.

The background image (`images/dracula-solid.png`) is mounted from the local `images/` directory.

---

## Screenshot

![Homepage Example](https://github.com/user-attachments/assets/ec8cd555-0528-4c93-a795-ab5867f5134b)

## Credits

- [gethomepage](https://github.com/gethomepage/homepage)
- Dracula theme by [Jas-SinghFSU](https://github.com/Jas-SinghFSU/homepage-dracula)
