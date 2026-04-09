# Ops Agent
*Server self-management, monitoring, service health, and infrastructure automation*

The agent that keeps the agentic server itself healthy. Watches everything, fixes what it can autonomously, escalates what it can't.

---

## Tools

| Tool                              | Why                                              |
| --------------------------------- | ------------------------------------------------ |
| Shell executor                    | System commands, service management, log queries |
| Docker / Podman API               | Container status, restart, resource usage        |
| Prometheus / Node Exporter        | CPU, RAM, disk, network metrics                  |
| Log aggregator (journald / Loki)  | Parse and search service logs                    |
| File reader/writer                | Read configs, write reports                      |
| cron / systemd timer manager      | Schedule recurring tasks                         |
| Notification channel              | Alerts and status reports                        |
| Web fetch                         | Check external reachability (uptime monitoring)  |
| Backup tool (restic / borgbackup) | Trigger and verify backups                       |
| DNS / domain checker              | TTL, record accuracy, expiry                     |

---

## Skills

### System Health
- **Health dashboard** — on-demand snapshot: CPU/RAM/disk/network, all running services, last 5 alerts
- **Resource trend analysis** — detect slow disk fill, memory leak patterns, abnormal CPU consumers over time
- **Service watchdog** — monitor critical services; auto-restart on crash; escalate to you if restart loop detected
- **Process anomaly detection** — flag unknown or unexpected processes, especially anything with high CPU/network unexpectedly
- **Temperature monitoring** — CPU/GPU temps if sensors available; alert on thermal throttling

### Container Management
- **Container health check** — list all containers, status, uptime, resource usage
- **Auto-restart unhealthy containers** — detect health-check failures; restart; notify
- **Image update scanner** — check for newer images of running containers; stage updates for your approval
- **Volume disk usage** — track Docker volume growth, flag ones growing fast

### Backups
- **Backup scheduler** — run configured backup jobs (restic/borg) on schedule
- **Backup integrity verifier** — periodically do a dry-run restore test; alert if backup is stale or corrupted
- **Backup report** — weekly summary: what was backed up, size, duration, next scheduled run

### Network & Connectivity
- **External uptime monitor** — ping your services from outside (or via uptime-kuma); alert on downtime
- **Port scan self-check** — periodic scan of own external footprint; alert on unexpected open ports (feeds into Cyber Agent)
- **DNS health check** — verify all your DNS records resolve correctly; detect misconfiguration early
- **Bandwidth usage report** — daily/weekly traffic summary per interface

### Automation & Maintenance
- **Log rotation enforcer** — ensure logs aren't filling disk; prune old logs per retention policy
- **Cron audit** — list all active cron jobs and systemd timers; flag ones that haven't run recently
- **OS update notifier** — check for available security patches; report without auto-applying (you decide)
- **Config drift detector** — hash critical config files; alert if they change unexpectedly

### Self-Healing Hierarchy
1. **Auto-fix** (no escalation): service restart, log rotation, temp file cleanup
2. **Auto-fix + notify**: container restart, backup retry
3. **Escalate immediately**: disk > 90%, unknown process, failed backup verification, service down after 3 restart attempts

---

## Agentic Server Self-Monitoring

Ops Agent also monitors the other agents:
- Track API cost per agent (daily/weekly spend)
- Alert if any agent exceeds cost threshold
- Report agent error rates and failure modes
- Restart hung agent processes
