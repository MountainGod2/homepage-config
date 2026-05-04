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

`{{HOMEPAGE_VAR_*}}` placeholders are substituted at build time from environment variables.

| .env.homepage |
|---|
| `HOMEPAGE_VAR_DOMAIN_NAME=example.com` |
| `HOMEPAGE_VAR_ROUTER_IP=192.168.0.1` |
| `HOMEPAGE_VAR_UNRAID_API_KEY="XXXXXXXXXXXXX"` |
| `HOMEPAGE_VAR_TAILSCALE_DEVICE_ID="XXXXXXXXXXXXX"` |
| `HOMEPAGE_VAR_TAILSCALE_API_KEY="XXXXXXXXXXXXX"` |
| etc. |

See [.env.homepage.sample](https://github.com/MountainGod2/homepage-config/blob/main/.secrets/.env.homepage.sample)
for the full list of variables.

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
