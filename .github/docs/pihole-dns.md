   Troubleshooting: The Port 53 Conflict
The Problem
During the initial deployment of Pi-hole, the container failed to start because Port 53 was already in use by the host system (systemd-resolved).

The Analysis
Ubuntu uses systemd-resolved as a local DNS stub listener. To allow Pi-hole to act as the primary DNS for the network, the host service had to be disabled to free up the socket.

The Solution
Stop the conflicting service:

sudo systemctl stop systemd-resolved
sudo systemctl disable systemd-resolved

Reconfigure Docker DNS:
Added an upstream DNS entry (8.8.8.8) to the Pi-hole docker-compose.yaml to ensure the container could still resolve external domains (like blocklist updates) before its own service was fully operational.
