# Architecture
*System design for the full agentic server stack*

---

## Layer Model

```
┌─────────────────────────────────────────────────────┐
│                    YOU (User)                        │
│         Telegram / ntfy / Voice / Web UI             │
└───────────────────────┬─────────────────────────────┘
                        │
┌───────────────────────▼─────────────────────────────┐
│              Meta-Orchestrator                       │
│   Routes tasks, resolves conflicts, manages queue    │
└──┬──────┬──────┬──────┬──────┬──────┬───────────────┘
   │      │      │      │      │      │
  Dev  Intel  Life  Cyber Health Finance  Ops  Knowledge
  Agent Agent Agent Agent Agent Agent   Agent  Agent
   │      │      │      │      │      │
┌──▼──────▼──────▼──────▼──────▼──────▼───────────────┐
│                  Shared Infrastructure                │
│   Memory │ Context Engine │ Tool Registry │ Audit Log │
└─────────────────────────────────────────────────────┘
```

---

## Meta-Orchestrator

The top-level router that handles incoming tasks and events.

**Responsibilities**
- Parse incoming message intent → route to correct agent
- Decompose multi-domain tasks (e.g. "research this tech and add it to my Obsidian" → Intelligence + Knowledge)
- Manage priority queue: urgent/normal/background
- Resolve conflicts (e.g. scheduling conflict between agents)
- Track cross-agent task state
- Enforce cost limits: stop agent chains that are burning too much API budget

**Routing logic**
```
Incoming task
  → classify domain (dev / intel / lifestyle / cyber / health / finance / ops / knowledge)
  → check priority (urgent / scheduled / background)
  → check dependencies (does this need output from another agent first?)
  → dispatch to agent(s), passing relevant context
  → await result
  → route result to output channel
```

---

## Memory System

Three layers, each with different retention and retrieval characteristics:

### 1. Working Memory (per-session)
- In-context window of active agent
- Ephemeral — cleared after session
- Contains: current task, recent messages, relevant retrieved context

### 2. Episodic Memory (event log)
- What happened, when, what was decided
- Stored as structured JSON + searchable
- Retention: 1 year rolling
- Enables: "what did I decide about X last month?", "what did the dev agent do on Tuesday?"

### 3. Semantic Memory (vector store)
- All notes, summaries, digests, and learned facts embedded as vectors
- Stored in: Qdrant (self-hosted) or ChromaDB
- Enables: semantic search across everything the system has ever processed
- Updated: continuously as new content arrives

---

## Context Engine

Injects relevant context into every agent session automatically.

**Personal context** (always injected)
- From `personal context.md` — user profile, preferences, communication style

**Domain context** (injected per agent)
- Dev: active repos, current sprint, open issues
- Health: current training phase, last session, weight trend
- Finance: current allocations, active watchlist
- etc.

**Dynamic context** (updated by events)
- Time of day (morning briefing vs evening review mode)
- Current project focus
- Upcoming events (fight in 3 weeks → health agent shifts to fight camp mode)

---

## Communication Infrastructure

### Channels
| Channel          | Use Case                                                                |
| ---------------- | ----------------------------------------------------------------------- |
| Telegram         | Primary two-way interface; per-agent bots or unified bot with /commands |
| ntfy             | Push alerts when Telegram isn't open (critical only)                    |
| Email            | Formal digests, reports you want to archive                             |
| Voice (optional) | Whisper STT → agent → TTS response for hands-free interaction           |

### Proactive vs Reactive
- **Reactive**: you message an agent, it responds
- **Proactive (scheduled)**: morning briefing, weekly review, CVE digest
- **Proactive (event-triggered)**: new GitHub issue → dev agent; flight price drop → lifestyle agent

### Notification Priority Tiers
1. **Critical** (ntfy + Telegram): service down, security alert, time-sensitive action needed
2. **Important** (Telegram): agent completed work, decision needed
3. **Informational** (Telegram digest or email): daily/weekly summaries

---

## Trigger System

How agents get activated beyond direct messages:

| Trigger Type   | Example                                                   |
| -------------- | --------------------------------------------------------- |
| Cron schedule  | Morning briefing at 07:00 daily                           |
| Webhook        | GitHub push event → dev agent                             |
| File watcher   | New note in Obsidian → knowledge agent indexes it         |
| Condition      | Disk > 85% → ops agent alert                              |
| Price alert    | BTC drops 10% → finance agent notify                      |
| Calendar event | Fight in 14 days → health agent activates fight camp mode |
|                |                                                           |

---

## Data Layer

| Store | Purpose | Technology |
|---|---|---|
| Vector DB | Semantic memory, note search | Qdrant (self-hosted) |
| Time-series DB | Metrics, biometrics, finance history | InfluxDB or Prometheus |
| Document store | Agent logs, episodic memory, reports | SQLite or PostgreSQL |
| File system | Obsidian vault, raw data files | Local FS |
| Secret store | API keys, credentials | Bitwarden / HashiCorp Vault |

---

## Model Routing

Not every task needs the most expensive model. Route by task complexity:

| Task Type                       | Model                     | Reason                  |
| ------------------------------- | ------------------------- | ----------------------- |
| Simple classification / routing | Minimax-M2.7 (fast)       | Cheap, fast enough      |
| Summaries, digests, drafts      | Minimax-M2.7              | Good quality/cost ratio |
| Complex reasoning, architecture | Sonnet / Opus             | Worth the cost          |
| Code generation / review        | Sonnet or Deepseek-Coder  | Code-specialized        |
| Embeddings                      | Local model (nomic-embed) | Free, private, fast     |

---

## Audit & Cost Tracking

Every agent action is logged:
```json
{
  "timestamp": "2026-04-08T09:30:00Z",
  "agent": "dev",
  "task_id": "abc123",
  "action": "spawned claude-code session",
  "model": "claude-sonnet-4-6",
  "input_tokens": 4200,
  "output_tokens": 1800,
  "cost_usd": 0.024,
  "outcome": "success"
}
```

Daily/weekly cost report surfaced by Ops Agent.
