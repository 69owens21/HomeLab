#  Monitoring & Observability (Uptime Kuma)

### Overview
Uptime Kuma serves as the lab's "heartbeat" monitor. It performs regular health checks on all internal services to ensure maximum availability for development.

### Monitor Configuration
| Monitor Name | Type | Target | Logic |
| :--- | :--- | :--- | :--- |
| **Gitea Service** | HTTP(s) | `git.home` | Success if Status 200 |
| **AI Backend** | HTTP(s) | `ai.home` | Checks Open WebUI availability |
| **DNS Gateway** | DNS | `192.168.4.201` | Verifies Pi-hole resolution |

### Alerting & Reliability
By tracking uptime percentages, this service identifies "noisy" containers or resource exhaustion issues before they impact the **LabSync** development workflow.
