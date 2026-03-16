# HomeLab

### Personal Homelab Infrastructure

A containerized, self-hosted environment for secure, local-first workflows and media automation.

## Project Overview

This repository contains the infrastructure-as-code (Docker Compose) and documentation for my private home lab. Built on **Ubuntu 24.04**, this environment serves as the development and staging ground for my Senior Capstone project, **LabSync**, various software engineering experiments, and a fully automated media streaming stack.

**Key Goals:**
* **Data Sovereignty:** Hosting all source code (Gitea) and documentation locally.
* **Privacy-First AI:** Running local LLMs (Ollama) to assist in code audits without data exfiltration.
* **Network Security:** Network-wide ad-blocking and DNS management via Pi-hole.
* **Infrastructure Monitoring:** Real-time health tracking of services via Uptime Kuma.
* **Automated Media Management:** Automated fetching, organizing, and hardware-accelerated streaming of media without DRM.
* **Secure Remote Access:** Zero-trust mesh networking to access local services remotely without exposing public ports.

---

## Architecture & Service Registry

| Service | Protocol/Host Port | URL (Local) | Purpose |
| :--- | :--- | :--- | :--- |
| **Pi-hole** | DNS / 80 | `http://pi.home` | DNS Ad-blocking & Local DNS |
| **Gitea** | HTTP / 3000 | `http://git.home` | Private Version Control |
| **Uptime Kuma** | HTTP / 3001 | `http://kuma.home` | Service Health Monitoring |
| **Open WebUI** | HTTP / 3002 | `http://ai.home` | Private LLM (Llama 3.2:1B) |
| **Homepage** | HTTP / 8080 | `http://home.lab` | Centralized Dashboard |
| **Stirling PDF** | HTTP / 8081 | `http://pdf.home` | Private PDF Toolkit |
| **Jellyfin** | HTTP / 8096 | `http://media.home` | Media Server & Streaming |
| **Sonarr** | HTTP / 8989 | `http://tv.home` | TV Show Automation |
| **Radarr** | HTTP / 7878 | `http://movies.home` | Movie Automation |
| **Prowlarr** | HTTP / 9696 | `http://index.home` | Indexer Manager |
| **qBittorrent** | HTTP / 8080 (VPN) | `http://dl.home` | P2P Download Client |
| **Gluetun** | WireGuard | N/A | Privacy Tunnel / VPN Gateway |
| **Tailscale** | WireGuard | N/A | Secure Mesh Network |

---

## Component Documentation
Detailed deployment configurations and security implementations for specific services:
* [Portainer Container Management](docs/portainer.md)
* [Jellyfin Media Server](docs/jellyfin.md)
* [Sonarr TV Automation](docs/sonarr.md)
* [Radarr Movie Automation](docs/radarr.md)
* [qBittorrent & Gluetun VPN](docs/qbittorrent.md)
* [Tailscale Mesh Network](docs/tailscale.md)

---

## Technical Challenges & Solutions

**1. The Port 53 Conflict (DNS Resolution)**
* **Challenge:** Ubuntu's `systemd-resolved` was occupying Port 53, preventing Pi-hole from starting.
* **Solution:** Disabled the host stub listener and configured the Docker container with upstream DNS (8.8.8.8) to ensure initial blocklist synchronization was successful before the local DNS was fully operational.

**2. Local LLM Optimization (CPU-Only)**
* **Challenge:** Providing responsive AI assistance without dedicated GPU hardware.
* **Solution:** Deployed Ollama using the Llama 3.2:1B model with 4-bit quantization. This achieved acceptable token-per-second rates on standard CPU hardware while maintaining enough context awareness to assist with Laravel and PHP debugging.

**3. Secure Service Discovery**
* **Challenge:** Accessing services via IP/Port is inefficient and hard to scale.
* **Solution:** Implemented a Reverse Proxy (Nginx Proxy Manager) paired with Pi-hole's Local DNS records to enable service discovery via friendly URLs (e.g., `git.home`).

**4. Resolving Container Permission Locks**
* **Challenge:** The official Jellyfin container encountered fatal `UnauthorizedAccessException` errors when attempting to write to host-mapped directories created by a non-root user.
* **Solution:** Migrated to LinuxServer.io base images for the entire media stack, mapping host user permissions explicitly via `PUID` and `PGID` environment variables to ensure robust file ownership across the container-host boundary.

**5. Securing Outbound P2P Traffic**
* **Challenge:** Preventing IP leaks during automated media downloads.
* **Solution:** Deployed the qBittorrent container completely sandboxed without a standard network interface, attaching it directly to the network namespace of a Gluetun (Mullvad VPN) container. This acts as a mandatory kill switch, cutting all traffic if the VPN drops.

---

## Getting Started

**Prerequisites:**
* Ubuntu 24.04 LTS
* Docker Engine & Docker Compose V2

**Installation:**
1. Clone the repository: `git clone https://github.com/69owens21/HomeLab.git`
2. Configure environment: `cp .env.example .env` (Update with your local IPs and secrets)
3. Deploy the stack: `docker compose up -d`

Created and maintained by Gracie Owens, 2026.
