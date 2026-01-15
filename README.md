# <img src="https://styleguide.torproject.org/static/images/tor-logo/color.svg" width="32"> Sapphive Tor Docker Image

![Docker Pulls](https://img.shields.io/docker/pulls/sapphive/tor) ![Docker Image Size](https://img.shields.io/docker/image-size/sapphive/tor) ![Build Status](https://github.com/sapphive/tor-docker/actions/workflows/build.yml/badge.svg)

⚠️ **UNOFFICIAL IMAGE** ⚠️

This is an unofficial Tor client image maintained by [SAPPHIVE](https://sapphive.com).
Built directly from the official [Tor Project repositories](https://deb.torproject.org/).
This project is **not** affiliated with, endorsed by, or sponsored by The Tor Project.

## Why use this image?

*   **Up-to-date:** Automatically rebuilt weekly to ensure the latest Tor version and security patches.
*   **Production-grade:** Includes healthchecks and runs as a non-root user.
*   **Official Sources:** Built using the Tor Project's own Debian repositories.

## Quick Start

### 🚀 Standard Client (Single Identity)
Ideal for basic anonymity and browsing. This is the slim version (~40MB).
```bash
docker run -d --name tor -p 9050:9050 sapphive/tor:latest
```

### 🔄 Rotating Proxy (Multi-Identity)
Ideal for web scraping and automated testing. It runs multiple Tor instances and load-balances between them for instant IP rotation.
```bash
docker run -d \
  --name tor-rotating \
  -p 9050:9050 \
  -e TOR_INSTANCES=10 \
  sapphive/tor:rotating
```

### 🧅 Onion Sidecar (Hidden Services)
Host your website or API on the darknet with zero configuration. This "sidecar" automatically generates a `.onion` address for any web service (Nginx, Apache, etc.).
```bash
docker run -d \
  --name tor-gate \
  -e TARGET=website_container:80 \
  -v ./tor-keys:/var/lib/tor/hidden_service \
  sapphive/tor:onion
```
Check the logs to find your `.onion` address: `docker logs tor-gate`

## ⚙️ Configuration

### Environment Variables

| Variable | Tag | Default | Description |
| :--- | :--- | :--- | :--- |
| `TOR_INSTANCES` | `rotating` | `10` | The number of independent Tor processes to run. |
| `TARGET` | `onion` | `localhost:80` | The internal address of the website to expose. |
| `ONION_PORT` | `onion` | `80` | The port your `.onion` site will listen on. |

### Advanced: Custom `torrc` (Standard Tag Only)
The standard image uses the default Tor configuration. You can mount your own `torrc` file:

```bash
docker run -d \
  --name tor \
  -p 9050:9050 \
  -v /path/to/your/torrc:/etc/tor/torrc:ro \
  sapphive/tor
```

## Maintainer

Maintained by [SAPPHIVE Support](mailto:support@sapphive.com) / [sapphive.com](https://sapphive.com).

## Legal

Tor is a trademark of The Tor Project, Inc. Use of the Tor trademark in this project is for descriptive purposes only.
