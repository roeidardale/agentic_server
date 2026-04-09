# Integrations
*MCP servers, APIs, and external services worth wiring in*

---

## MCP Servers (Priority Order)

MCP (Model Context Protocol) gives agents direct, structured tool access to external systems.

### Tier 1 — High Value, Wire In Early

| MCP Server              | Agent(s)                | What It Unlocks                                      |
| ----------------------- | ----------------------- | ---------------------------------------------------- |
| **GitHub MCP**          | Dev                     | Issues, PRs, code review, comments, webhooks         |
| **Obsidian MCP**        | Knowledge, Intelligence | Direct vault read/write without file system hacks    |
| **Google Calendar MCP** | Lifestyle, Health       | Event read/write, fight camp scheduling, reminders   |
| **Telegram Bot API**    | All                     | Primary communication channel for all agents         |
| **Filesystem MCP**      | All                     | Structured local file access with permission scoping |

### Tier 2 — Add When Relevant

| MCP Server            | Agent(s)   | What It Unlocks                                          |
| --------------------- | ---------- | -------------------------------------------------------- |
| **Docker MCP**        | Ops        | Container management without raw shell                   |
| **Prometheus MCP**    | Ops        | Query metrics programmatically                           |
| **Linear / Jira MCP** | Dev        | Task/sprint management beyond GitHub issues              |
| **Notion MCP**        | Knowledge  | If you ever use Notion alongside Obsidian                |
| **Gmail MCP**         | Lifestyle  | Email read/draft (already available in this environment) |
| **Bitwarden MCP**     | All        | Secret retrieval for agent credentials                   |
| **Cloudflare MCP**    | Ops, Cyber | DNS management, firewall rules, analytics                |

### Tier 3 — Nice to Have

| MCP Server             | Agent(s)     | What It Unlocks                                    |
| ---------------------- | ------------ | -------------------------------------------------- |
| **Spotify MCP**        | Lifestyle    | Mood-based music, focus playlists during deep work |
| **Home Assistant MCP** | Lifestyle    | Smart home control, environment triggers           |
| **Grafana MCP**        | Ops          | Dashboard queries, alert management                |
| **Discord MCP**        | Intelligence | Monitor tech communities, surface relevant threads |
| **Reddit MCP**         | Intelligence | Subreddit monitoring for your interest areas       |
| **Proxmox MCP**        | Ops          | VM/LXC management if running hypervisor            |

---

## APIs (No MCP, Direct Integration)

### Security & Cyber
| API | Agent | Use |
|---|---|---|
| Shodan | Cyber | Infrastructure exposure scanning |
| VirusTotal | Cyber | File/URL reputation |
| NVD / CVE API | Cyber, Dev | Vulnerability monitoring |
| Have I Been Pwned | Cyber | Account breach monitoring |

### Finance & Markets
| API | Agent | Use |
|---|---|---|
| CoinGecko | Finance | Crypto prices, portfolio valuation |
| Alpha Vantage / Yahoo Finance | Finance | Stock/ETF data |
| CoinMarketCap | Finance | Market cap, dominance, trending |
| Binance / Kraken API | Finance | Live portfolio from exchange |

### Research & Intelligence
| API | Agent | Use |
|---|---|---|
| arXiv API | Intelligence | Paper search and fetch |
| HN Algolia API | Intelligence | Hacker News search and trending |
| GitHub Trending (scraper) | Intelligence | Trending repos by language/topic |
| RSS feeds (custom list) | Intelligence | Tech blogs, security advisories |
| YouTube Data API | Intelligence | Transcript fetching, channel monitoring |

### Health & Biometrics
| API | Agent | Use |
|---|---|---|
| Edamam Nutrition API | Health | Macro/micronutrient lookups |
| Open-Meteo (weather) | Health, Lifestyle | Training conditions, outdoor planning |
| Garmin Connect API | Health | Training data if using Garmin |
| Whoop API | Health | HRV, recovery score, sleep if using Whoop |
| Oura Ring API | Health | Sleep staging, readiness if using Oura |

### Infrastructure
| API | Agent | Use |
|---|---|---|
| ntfy (self-hosted) | Ops, All | Push notifications without phone number |
| Uptime Kuma API | Ops | External service monitoring |
| Restic REST server | Ops | Backup management |
| Tailscale API | Ops, Cyber | VPN/overlay network management |

---

## Self-Hosted Stack Recommendation

Services worth running locally on the agentic server:

| Service | Purpose |
|---|---|
| **Qdrant** | Vector database for semantic memory |
| **ntfy** | Push notification server |
| **Uptime Kuma** | Service uptime monitoring |
| **Grafana + Prometheus** | Metrics visualization |
| **Loki + Promtail** | Log aggregation |
| **Gitea / Forgejo** | Self-hosted git (for private repos) |
| **Vaultwarden** | Self-hosted Bitwarden |
| **Whisper (local)** | STT for voice input |
| **Ollama** | Local LLM for cheap/private tasks (embeddings, classification) |
| **n8n** | Workflow automation and webhook routing |
