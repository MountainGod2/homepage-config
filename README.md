# Homepage Config

My personal configuration files for [gethomepage/homepage](https://github.com/gethomepage/homepage/).

## Getting Started

### Prerequisites

- **Docker** installed on your system ([Install Docker](https://docs.docker.com/get-docker/)).
- A user-defined Docker network for your containers (create one with `docker network create my-network`).
- A `.env.homepage` file with required environment variables.

### Setup

1. Clone this repository:
   ```bash
   git clone https://github.com/MountainGod2/homepage_config.git
   cd homepage_config
   ```

2. Create a `.env.homepage` file in the appropriate directory. Example:
   ```env
   HOMEPAGE_VAR_SERVER_IP=192.168.0.100
   HOMEPAGE_VAR_DOMAIN_NAME=example.com
   HOMEPAGE_VAR_CLOUDFLARE_ACCOUNT_ID=XXXX
   ```

3. Run the Docker container using the provided commands.

---

## Configuration Examples

### Docker Run Command

#### Using a `.env.homepage` File

```bash
docker run \
  -d \
  --name='homepage' \
  --net='dsn' \
  --env-file /path/to/homepage/.secrets/.env.homepage \
  -e TZ="America/Denver" \
  -p '3000:3000/tcp' \
  -v '/path/to/homepage/config:/app/config:rw' \
  -v '/path/to/homepage/icons:/app/icons:rw' \  # Optional mount for local icons
  -v '/path/to/homepage/images:/app/images:rw' \  # Optional mount for local background images
  -v '/mnt/':'/mnt':'ro' \  # Optional mount for local disk statistics
  'ghcr.io/gethomepage/homepage:latest'
```

#### Setting Environment Variables Inline

```bash
docker run \
  -d \
  --name='homepage' \
  --net='dsn' \
  -e 'HOMEPAGE_VAR_SERVER_IP=192.168.0.100' \
  -e 'HOMEPAGE_VAR_DOMAIN_NAME=example.com' \
  -e 'HOMEPAGE_VAR_CLOUDFLARE_ACCOUNT_ID=XXXX' \
  -p '3000:3000/tcp' \
  -v '/path/to/homepage/config:/app/config:rw' \
  -v '/path/to/homepage/icons:/app/icons:rw' \  # Optional mount for local icons
  -v '/path/to/homepage/images:/app/images:rw' \  # Optional mount for local background images
  -v '/mnt/':'/mnt':'ro' \  # Optional mount for local disk statistics
  'ghcr.io/gethomepage/homepage:latest'
```

### Environment Variables

| Variable                             | Description                            |
|--------------------------------------|----------------------------------------|
| `HOMEPAGE_VAR_SERVER_IP`             | The IP address of the server.          |
| `HOMEPAGE_VAR_DOMAIN_NAME`           | The domain name for the services.      |
| `HOMEPAGE_VAR_CLOUDFLARE_ACCOUNT_ID` | Cloudflare account ID for integration. |
| `HOMEPAGE_VAR_TAILSCALE_API_KEY`     | API key for Tailscale integration.     |
| ...                                  | ...                                    |

---

## Custom Theme

To enable the included Dracula theme:

1. Copy `config/custom.css` to your `config` directory.
2. Update your `settings.yaml` to include:
   ```yaml
   theme: dark
   color: gray
   background: /images/dracula-solid.png
   ```

For more themes, check [homepage-dracula](https://github.com/Jas-SinghFSU/homepage-dracula).

---

## Screenshots

![Homepage Example](https://github.com/user-attachments/assets/ec8cd555-0528-4c93-a795-ab5867f5134b)

## Credits

- [gethomepage](https://github.com/gethomepage/homepage)
- Dracula Theme by [Jas-SinghFSU](https://github.com/Jas-SinghFSU/homepage-dracula)
