# Secure Mesh Network (Tailscale)

## Overview
Tailscale provides a zero-config, WireGuard-based mesh VPN for the homelab. It allows seamless, encrypted remote access to internal services without exposing any ports to the public internet.

## Key Use Cases
* **Remote Streaming:** Accessing the Jellyfin dashboard and media streams remotely from mobile devices or laptops while traveling.
* **Infrastructure Management:** Securely SSH-ing into the host or accessing Portainer from outside the local network.
* **MagicDNS Integration:** Routing traffic using simple hostnames instead of tracking shifting IP addresses.

## Security Implementation
* **Zero Public Exposure:** Eliminates the need for port forwarding on the physical router, effectively hiding the server from public internet scanning bots.
* **End-to-End Encryption:** Utilizes the WireGuard protocol to secure all node-to-node traffic automatically.
* **Identity-Based Auth:** Tied directly to a secure identity provider with mandatory key authentication for any new device joining the mesh.
