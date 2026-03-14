# HomeLab

# Personal Homelab Infrastructure
**A containerized, self-hosted development environment for secure, local-first workflows.**

## Project Overview
This repository contains the infrastructure-as-code (Docker Compose) and documentation for my private home lab. Built on **Ubuntu 24.04**, this environment serves as the development and staging ground for my Senior Capstone project, **LabSync**, and various software engineering experiments.

### Key Goals:
* **Data Sovereignty:** Hosting all source code (Gitea) and documentation locally.
* **Privacy-First AI:** Running local LLMs (Ollama) to assist in code audits without data exfiltration.
* **Network Security:** Network-wide ad-blocking and DNS management via Pi-hole.
* **Infrastructure Monitoring:** Real-time health tracking of services via Uptime Kuma.

---

## Architecture & Service Registry



| Service | Protocol | Host Port | URL (Local) | Purpose |
| :--- | :---: | :---: | :--- | :--- |
| **Pi-hole** | DNS/HTTP | `80` | `http://pi.home` | DNS Ad-blocking & Local DNS |
| **Gitea** | Git/HTTP | `3000` | `http://git.home` | Private Version Control |
| **Uptime Kuma** | HTTP | `3001` | `http://kuma.home` | Service Health Monitoring |
| **Open WebUI** | HTTP | `3002` | `http://ai.home` | Private LLM (Llama 3.2:1B) |
| **Homepage** | HTTP | `8080` | `http://home.lab` | Centralized Dashboard |
| **Stirling PDF**| HTTP | `8081` | `http://pdf.home` | Private PDF Toolkit |

---

## Technical Challenges & Solutions

### 1. The Port 53 Conflict (DNS Resolution)
**Challenge:** Ubuntu's `systemd-resolved` was occupying Port 53, preventing Pi-hole from starting.
**Solution:** Disabled the host stub listener and configured the Docker container with upstream DNS (8.8.8.8) to ensure initial blocklist synchronization was successful before the local DNS was fully operational.

### 2. Local LLM Optimization (CPU-Only)
**Challenge:** Providing responsive AI assistance without dedicated GPU hardware.
**Solution:** Deployed **Ollama** using the `Llama 3.2:1B` model with 4-bit quantization. This achieved acceptable token-per-second rates on standard CPU hardware while maintaining enough context awareness to assist with Laravel and PHP debugging.

### 3. Secure Service Discovery
**Challenge:** Accessing services via IP/Port is inefficient and hard to scale.
**Solution:** Implemented a **Reverse Proxy** (Nginx Proxy Manager) paired with Pi-hole's Local DNS records to enable service discovery via friendly URLs (e.g., `git.home`).

---

## Getting Started

### Prerequisites:
* Ubuntu 24.04 LTS
* Docker Engine & Docker Compose V2

### Installation:
1. **Clone the repository:**
   `git clone https://github.com/69owens21/HomeLab.git`
2. **Configure environment:**
   `cp .env.example .env` (Update with your local IPs and secrets)
3. **Deploy the stack:**
   `docker compose up -d`
---
*Created and maintained by Gracie Owens, 2026.*
