## Dev Domain

The Dev domain is split into two layers: the **hermes Orchestrator** (decides, delegates, validates, reports) and **Claude Code** (executes). The orchestrator never touches code directly — it picks the right Claude Code profile for the job, watches the session, and keeps you in the loop.

---

### hermes Dev Orchestrator
**Purpose**
Observer and coordinator of Claude Code sessions. Pulls work from GitHub, decides which Claude Code profile fits the task, assembles context, monitors the session, validates results, and surfaces a clean debrief to you before anything is acted on.

**Tools**
| Tool | Why |
|---|---|
| GitHub/GitLab API | Pull issues, PRs, review threads, post back results |
| Claude Code CLI | Spawn, monitor, interrupt, and terminate sessions |
| Git (read-only) | Inspect diffs Claude Code produced before surfacing to you |
| Test runner (rea) | Check pass/fail after a session completes |
| Notification channel | Alert you at key checkpoints (Telegram, ntfy, email) |
| Task/work queue | Track what's pending, in-progress, done across sessions |

**Skills**
- **Issue intake** — pull a GitHub issue, gather related files/history/linked PRs, craft a focused Claude Code prompt
- **Profile selection** — match the task type to the right Claude Code profile (see below)
- **Session monitoring** — watch Claude Code output in real time, detect drift or stalls
- **Human escalation** — pause and notify you when a decision is destructive, ambiguous, or confidence is low
- **Change validation** — after a session, check test results and diff scope before surfacing to you
- **PR orchestration** — open a draft PR with a plain-English summary, tag you for review — never auto-merge
- **Multi-session coordination** — run parallel sessions for independent tasks, sequence dependent ones
- **Session debrief** — produce a short summary of what changed, why, and what still needs human attention

---

### Claude Code — Profiles

The orchestrator picks a profile when spawning a session. Each profile is a defined set of tools and a focused system prompt loaded into Claude Code for that task type.

---

#### Profile: Code Review

**Purpose** — Analyze a diff or PR and produce a structured review.

**Tools loaded into Claude Code**
- File reader (read relevant source files for context)
- Git diff viewer
- Codebase search / grep (trace usages, find related logic)
- GitHub PR API (read existing comments, post inline review comments)

**Skills**
- Summarize what a PR does in plain English
- Flag bugs, logic errors, and security issues with line references
- Identify missing tests or edge cases- Note style/convention deviations without being pedantic
tructured review comment back to GitHub

---

#### Profile: Bug Fix / Debug

- [ ] **Purpose** — Given a bug report or error trace, reproduce, narrow root cause, and write a targeted fix.

**Tools loaded into Claude Code**
- File read/write
-it (diff, log, blame — understand recent changes near the bug)
- Shell executor (run tests, reproduce the failure)
- Web search + fetch (look up errors, docs, known issues)

**Skills**
- Reproduce failure from a trace or description
- Use blame/log to identify when and where regression was introduced
- Write a minimal targeted fix — no scope creep
- Write a regression test covering the fixed case
- Summarize root cause for the orchestrator's debrief

---

#### Profile: Feature Development

**Purpose** — Implement a scoped feature from a spec or issue description.

**Tools loaded into Claude Code**
- File read/write
- Git (branch, diff, status)
- Shell executor (run build, tests, linters)
- Web search + fetch (docs, API references)
- Package manager (npm/pip/cargo — add dependencies if needed)

**Skills**
- Parse a spec or issue into implementation steps before writing any code
- Implement incrementally, running tests at each step
- Handle edge cases explicitly stated in the spec
- Write tests alongside the feature, not after
- Flag anything underspecified back to the orchestrator rather than guessing

---

#### Profile: efactor

**Purpose** — Restructure existing code without changing behavior.

**Tools loaded into Claude Code**
- File read/write
- Codebase search / grep (find all usages before renaming or moving)
- Git (diff — keep changes reviewable and scoped)
- Shell executor (run full test suite after each change)

**Skills**
- Map all call sites before touching anything
- Make one logical change at a time, verify tests pass between steps
- Produce a clean, reviewable diff — no noise
- Never change behavior as part of a refactor; flag it separately if spotted

---

#### Profile: Scaffolding

**Purpose** — Generate a new project or module skeleton from a description.

**Tools loaded into Claude Code**
- File write
- Shell executor (init commands, install deps, run scaffold tools)
- Web fetch (reference latest conventions, starter docs)
- Package manager

**Skills**
- Produce a minimal, working scaffold — not an over-engineered template
- Configure tooling (linter, formatter, test runner, CI stub)
- Install only explicitly needed dependencies
- Output a brief summary of what was created and how to run it

---

#### Profile: Documentation

**Purpose** — Generate or update docs from existing source code.

**Tools loaded into Claude Code**
- File read/write
- Codebase search (discover all public API surfaces)
- Git log (understand change history for changelog/release notes)

**Skills**
- Generate README from project structure and entry points
- Write API docs from function signatures and usage patterns
- Produce architecture overview from file/module structure
- Write changelog entries from git log between tags

---

#### Profile: Dependency & Security Audit

**Purpose** — Identify outdated, vulnerable, or unnecessary dependencies and produce actionable output.

**Tools loaded into Claude Code**
- File reader (package manifests)
- Shell executor (run `npm audit`, `pip-audit`, `cargo audit`)
- Package registry APIs (npm, PyPI, crates.io — latest versions)
- CVE / GitHub Advisory API (known vulnerabilities)
- Git (open a branch for upgrade PRs)

**Skills**
- List all outdated deps with current vs latest version
- Flag any with known CVEs, with severity
- Group into: safe-to-auto-upgrade, needs-testing, breaking-change
- Open one PR per upgrade group, not one giant PR
- Summarize risk level for the orchestrator to report to you

---
