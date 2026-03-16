# TV Automation (Sonarr)

## Overview
Sonarr acts as the personal video recorder (PVR) for television shows. It monitors RSS feeds for new episodes, interfaces with indexers, and coordinates with download clients to retrieve and organize media automatically.

## Key Use Cases
* **Release Fetching:** Automatically grabbing new episodes of monitored shows as soon as they are available.
* **Library Management:** Renaming downloaded files to standard naming conventions and moving them into the Jellyfin media directories.
* **Quality Control:** Upgrading existing episodes dynamically when better quality rips (e.g., Web-DL to BluRay) become available.

## Security Implementation
* **Internal Routing:** Binds exclusively to internal Docker networks; external access is managed through a secure reverse proxy or VPN.
* **API Authentication:** Communication with external indexers (via Prowlarr) is strictly secured using internal API keys.
