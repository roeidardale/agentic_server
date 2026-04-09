# Skills Roadmap
*Additions to existing agents: Dev, Intelligence, Lifestyle*

---

## Dev Agent — Additional Skills

### For the Orchestrator
| Skill                        | Description                                                                                                            |
| ---------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| **Webhook listener**         | Receive GitHub events (push, PR open, issue created) and auto-trigger the right Claude Code profile                    |
| **Multi-repo context**       | Maintain a map of active repos — when a task references a repo, auto-inject its README, tech stack, and recent history |
| **Technical debt tracker**   | Periodic scan across repos; score and trend debt (TODOs, complexity, test coverage)                                    |
| **CI/CD pipeline monitor**   | Watch build/test results; alert on persistent failures; auto-open bug task if main branch red for > 1h                 |
| **Commit message generator** | After a Claude Code session, draft a conventional commit message from the diff                                         |
| **Release notes generator**  | Given a tag range, produce structured release notes from commits + linked issues                                       |
| **Code quality dashboard**   | Weekly report: test coverage trend, lint errors, complexity metrics across tracked repos                               |

### New Claude Code Profile: Test Writer
**Purpose** — Given existing code with no tests, write a comprehensive test suite.

**Tools**: File reader, shell executor (run tests), codebase search
**Skills**:
- Analyze code for testable units and edge cases
- Write unit + integration tests
- Achieve meaningful coverage without testing implementation details
- Run suite and fix failures before reporting done

### New Claude Code Profile: Migration
**Purpose** — Database migrations, API version upgrades, framework upgrades.

**Tools**: File read/write, shell executor, git, web fetch (docs)
**Skills**:
- Audit all affected call sites before changing anything
- Migrate incrementally with tests at each step
- Produce rollback plan alongside migration
- Flag breaking changes that require manual decisions

---

## Intelligence Agent — Additional Skills

| Skill | Description |
|---|---|
| **Podcast monitor** | Track subscribed podcasts; fetch new episodes; summarize transcripts; extract key insights |
| **Patent search** | Search USPTO/EPO for patents in a technology area; surface relevant prior art |
| **Author tracker** | Follow specific researchers; alert when they publish new papers or post on arXiv |
| **Technology radar** | Categorize technologies you encounter into: Adopt / Trial / Assess / Hold; track changes over time |
| **Competitive analysis** | Given a product/company, produce a structured breakdown: features, pricing, strengths, weaknesses |
| **Repo deep-dive** | Given a GitHub URL, produce an architectural tour: structure, key abstractions, how to contribute |
| **Terminology explainer** | Explain any concept at "expert" or "beginner" level on demand — defaults to your level (expert) |
| **Trend momentum score** | For tracked technologies, compute momentum (GitHub stars/week, mentions/week, job postings); surface rising vs declining |
| **Conference tracker** | Monitor major tech/security/MMA-related conferences; flag relevant talks; fetch slides/recordings post-event |

---

## Lifestyle Agent — Additional Skills

| Skill | Description |
|---|---|
| **Habit tracker** | Log daily habits (training, reading, nutrition); visualize streaks and consistency |
| **Weekly review generator** | Auto-pull data from all agents; produce a structured weekly review: wins, misses, focus for next week |
| **Goal tracking (OKR-style)** | Set quarterly objectives with key results; weekly check-in on progress; alert on at-risk KRs |
| **Decision journal** | Structured intake for important decisions: options, reasoning, expected outcome; reviewed after outcome known |
| **Focus mode** | On demand: block distracting sites/notifications, set a timer, notify when session ends |
| **Social calendar manager** | Track people you want to stay in touch with; surface "haven't talked to X in 3 months" reminders |
| **Meeting prep brief** | Before any calendar event, auto-generate a brief: who's attending, context, what to prepare |
| **Price tracker** | Monitor items on watchlist (electronics, equipment, etc.); alert on price drops |
| **Travel assistant** | Given a destination and date, research: visa requirements, weather, packing list, logistics |
| **Evening wind-down** | End-of-day routine: log top 3 wins, tomorrow's top priorities, anything unresolved — write to knowledge base |

---

## Cross-Agent Skills

Skills that span multiple agents and require coordination:

| Skill | Agents Involved | Description |
|---|---|---|
| **Morning briefing** | Lifestyle + Health + Finance + Intel | Unified daily brief: weather, schedule, training readiness, market snapshot, top news |
| **Weekly synthesis** | All agents | Every Sunday: what happened across all domains, decisions made, things to review |
| **Context sync** | All agents | When major context changes (new job, new fight booked, moving cities), update all agents' context simultaneously |
| **Goal alignment check** | Dev + Finance + Health + Lifestyle | Monthly: are your daily actions aligned with your stated goals? Surface misalignments |
| **Deep work scheduler** | Dev + Lifestyle + Health | Block optimal deep work windows based on: calendar, training load, energy patterns |
