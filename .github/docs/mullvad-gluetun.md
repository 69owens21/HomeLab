# Privacy Tunnel (Gluetun / Mullvad)

## Overview
Gluetun is a lightweight VPN client wrapper used to route specific Docker container traffic through Mullvad VPN. It provides a secure, encrypted tunnel for outbound infrastructure traffic.

## Key Use Cases
* **Traffic Obfuscation:** Encrypting outbound requests from download clients to prevent ISP throttling or tracking.
* **Network Gateway:** Acting as the primary network interface for dependent containers (e.g., qBittorrent), ensuring they cannot communicate if the VPN drops.
* **Port Mapping:** Handling internal port forwarding for services routed through the secure tunnel.

## Security Implementation
* **Strict Kill Switch:** Designed to drop all routed traffic immediately if the connection to Mullvad is lost, preventing IP leaks.
* **Local Network Sharing:** Configured to allow specific LAN subnets, maintaining local dashboard access while outbound traffic remains encrypted.
