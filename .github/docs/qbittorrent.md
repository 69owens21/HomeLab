# Download Client (qBittorrent)

## Overview
qBittorrent is the primary peer-to-peer (P2P) download client for the media stack. It is a highly efficient, open-source BitTorrent client that interfaces directly with Sonarr and Radarr to process requested media files.

## Key Use Cases
* **Automated Processing:** Catching torrents and magnet links sent via API from the automation applications (*arr stack).
* **Download Management:** Handling active peers, managing seeding ratios, and temporarily storing media files before they are renamed and moved to the permanent library.
* **Queue Health:** Automatically pausing, resuming, or dropping dead torrents based on predefined logic.

## Security Implementation
* **Traffic Routing (Kill Switch):** The container is deployed without its own network interface. Instead, it is bound directly to the `gluetun` (Mullvad VPN) container (`network_mode: "service:gluetun"`). If the VPN tunnel drops, qBittorrent immediately loses all internet access, completely preventing IP leaks.
* **Authentication:** The Web UI is protected by mandatory local authentication to prevent unauthorized access to the download queue.
* **Non-Root Execution:** Utilizes `PUID` and `PGID` environment variables via the LinuxServer image to ensure downloaded files have the correct host permissions for seamless media transfer.
