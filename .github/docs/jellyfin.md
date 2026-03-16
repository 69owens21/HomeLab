# Media Server (Jellyfin)

## Overview
Jellyfin is the core media server for this homelab. It organizes, serves, and streams local video content to various devices without DRM or licensing restrictions. It is configured to utilize the LinuxServer.io image for reliable permission handling.

## Key Use Cases
* **Media Streaming:** Serving TV shows and movies to local and remote endpoints, including handheld gaming PCs and mobile devices.
* **Hardware Transcoding:** Utilizing NVIDIA NVENC via Docker device reservations to offload video encoding from the CPU, ensuring smooth playback on devices that lack native format support.
* **Metadata Management:** Automatically scraping and organizing posters, cast info, and subtitles for the local library.

## Security Implementation
* **User Isolation:** Runs non-root by explicitly mapping `PUID` and `PGID` environment variables to prevent container breakout and host-level permission locks.
* **Remote Access:** Exposed externally only via secure mesh VPN (Tailscale) rather than direct port forwarding.
