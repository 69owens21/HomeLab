Network & Infastructure Map

This document outlines the logical network structure of the home lab, including port assignments and service discovery.

| Service | Internal Port | External Port | URL (Local) | Purpose |
| :--- | :---: | :---: | :--- | :--- |
| **Pi-hole** | `80` | `80` | `http://pi.home` | DNS-level Ad-blocking |
| **Gitea** | `3000` | `3000` | `http://git.home` | Local Source Control |
| **Uptime Kuma** | `3001` | `3001` | `http://kuma.home` | Service Monitoring |
| **Open WebUI** | `8080` | `3002` | `http://ai.home` | Private LLM Interface |
| **Homepage** | `3000` | `8080` | `http://home.lab` | Central Dashboard |

Service Discovery

The lab utilizes Pi-hole for local DNS resolution and Nginx Proxy Manager (Reverse Proxy) to route traffic from friendly URLs (e.g., ai.home) to specific container ports.
