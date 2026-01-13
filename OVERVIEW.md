# Sapphive Tor Client

![Docker Pulls](https://img.shields.io/docker/pulls/sapphive/tor) ![Docker Image Size](https://img.shields.io/docker/image-size/sapphive/tor) ![Build Status](https://github.com/sapphive/tor-docker/actions/workflows/build.yml/badge.svg)

⚠️ **UNOFFICIAL IMAGE**
*This is an unofficial Tor client image maintained by [SAPPHIVE](https://sapphive.com). It is built directly from official [Tor Project repositories](https://deb.torproject.org/). This project is not affiliated with, endorsed by, or sponsored by The Tor Project.*

---

## 🚀 Overview

This image provides a production-hardened, automatically updated Tor client. It is designed for developers and DevOps teams who need a reliable, up-to-date Tor SOCKS5 proxy without the maintenance overhead.

### Key Features:
*   🛡️ **Security Hardened:** Runs as a non-root user (`debian-tor`).
*   🔄 **Fully Automated:** Rebuilt weekly to ensure the latest Tor binary and OS security patches.
*   🩺 **Integrated Healthchecks:** Periodic internal checks verify the SOCKS5 proxy is active.
*   📦 **Multi-Arch Support:** Optimized for `amd64` (Intel/AMD) and `arm64` (Apple Silicon/Raspberry Pi).

---

## 🛠️ Usage

### Quick Start (Docker CLI)
Run the latest stable version with one command:
```bash
docker run -d \
  --name tor-client \
  -p 9050:9050 \
  sapphive/tor:latest
```

### Infrastructure (Docker Compose)
Recommended for production environments:
```yaml
services:
  tor:
    image: sapphive/tor:stable
    container_name: tor-proxy
    ports:
      - "9050:9050"
    restart: always
    healthcheck:
      test: ["CMD", "curl", "--socks5-hostname", "localhost:9050", "https://check.torproject.org/"]
      interval: 60s
      timeout: 15s
      retries: 3
```

---

## ⚙️ Configuration

### Custom Tor Config (`torrc`)
By default, this image exposes the SOCKS port on `0.0.0.0:9050`. To use a custom configuration:
```bash
docker run -d \
  -p 9050:9050 \
  -v /path/to/your/torrc:/etc/tor/torrc:ro \
  sapphive/tor
```

---

## 🏷️ Supported Tags
*   `latest`, `stable`: Always points to the most recent weekly build.
*   `0.4.x.x`: Specific Tor versions for high-stability environments.

---

## 🤝 Maintainer & Support
Maintained by **SAPPHIVE Infrastructure Team**.
*   **Website:** [sapphive.com](https://sapphive.com)
*   **Support:** [support@sapphive.com](mailto:support@sapphive.com)
*   **Source:** [GitHub: sapphive/tor-docker](https://github.com/sapphive/tor-docker)

## ⚖️ Legal Disclaimer
Tor is a trademark of The Tor Project, Inc. Use of the Tor trademark is for descriptive purposes only.
