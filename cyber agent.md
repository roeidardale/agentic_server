# Cyber Agent
*Security research, OSINT, infrastructure hardening, and CTF assistance*

Given your background in cyber — this agent operates in an explicitly authorized/personal scope only.

---

## Tools

| Tool                                 | Why                                            |
| ------------------------------------ | ---------------------------------------------- |
| Shodan / Censys API                  | Surface exposure of your own infra             |
| Nmap wrapper                         | Scan own network, track port changes over time |
| CVE / NVD API                        | Monitor CVEs relevant to your stack            |
| OSINT framework (theHarvester, etc.) | Research targets (authorized)                  |
| VirusTotal API                       | Hash/URL/file reputation checks                |
| Metasploit RPC (sandboxed)           | CTF/lab exploit development                    |
| Web fetch + scraper                  | Security blogs, advisories, exploit-db         |
| File reader                          | Analyze configs, certs, firewall rules         |
| Shell executor                       | Run local audit tools (lynis, trivy, etc.)     |
| Note writer                          | Save findings to knowledge base                |

---

## Skills

- **Infrastructure exposure audit** — scan your own external footprint, diff against previous scan, alert on new open ports or misconfigs
- **CVE watch** — daily check of CVEs affecting your installed software stack; severity-ranked summary to your channel
- **CTF assistant** — given a challenge file or description, enumerate attack surface, suggest techniques, execute in a sandboxed shell
- **Config hardening review** — audit SSH config, firewall rules, nginx/caddy configs, docker socket exposure against hardening benchmarks
- **Secret leak scanner** — scan your repos and dotfiles for accidentally committed credentials, API keys, private keys
- **Dependency vulnerability map** — cross-reference your full software inventory against known CVEs (complements Dev Agent's audit profile)
- **OSINT target report** — given a domain or company (your own, or authorized pentest target), produce a structured recon summary
- **Incident response helper** — given a suspicious log snippet or alert, triage, suggest containment steps, draft incident report
- **Cert & TLS monitor** — track expiry dates on all your domains/services, alert 30d/7d/1d before expiry
- **Red/Blue drills** — periodically simulate attack scenarios against your own homelab and report gaps

---

## Modes

| Mode | Behavior |
|---|---|
| Passive (default) | Monitor, alert, report — no active scanning |
| Active | Authorized scans of own infra on demand |
| Lab / CTF | Full tooling unlocked, sandboxed environment |

---

## Notes

- All active scanning strictly scoped to own infrastructure or explicitly authorized targets
- Results stored encrypted in knowledge base
- Sensitive findings go to private channel only, not shared logs
