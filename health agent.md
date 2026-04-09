# Health & Performance Agent
*MMA training, strength, nutrition, recovery, and biometric tracking*

Built around your actual life: competitive MMA + a drive for peak performance. Not generic wellness — sport-specific optimization.

---

## Tools

| Tool | Why |
|---|---|
| Training log file reader | Parse and store sessions (CSV, JSON, or free text) |
| Nutrition DB API (Edamam / USDA) | Macro/micronutrient lookups |
| Weather API | Factor training conditions |
| Calendar API | Schedule training blocks, recovery days, fight camp phases |
| Web search + scraper | Latest sports science, MMA conditioning research |
| PDF reader | Research papers, training programs |
| Note writer | Store PRs, session notes, body metrics |
| Notification channel | Daily check-ins, alerts, reminders |
| Wearable API (Garmin / Whoop / Oura, optional) | HRV, sleep, resting HR if device available |

---

## Skills

### Training Management
- **Session logger** — structured intake of today's session (type, duration, intensity, notes); writes to training log
- **Weekly volume tracker** — sum load across striking, grappling, strength, conditioning; flag overreach vs underload
- **Fight camp planner** — given a fight date, build a periodized camp (general → specific → taper → fight week)
- **Deload detector** — analyze cumulative fatigue indicators, recommend deload timing before you need to ask
- **Skill gap analysis** — based on logged sessions and notes, surface which areas (takedowns, clinch, footwork, etc.) are getting undertrained
- **Training split optimizer** — given your schedule constraints, suggest optimal weekly split

### Nutrition
- **Meal macro calculator** — given foods eaten (free text input), estimate macros and flag any major shortfalls
- **Cut/bulk advisor** — given current weight and target, calculate deficit/surplus, expected timeline, and alert if rate is too aggressive
- **Weight cut planner** — if you're cutting for a fight, day-by-day water/carb protocol (evidence-based, not dangerous)
- **Supplement stack tracker** — log supplements taken, flag timing issues or interactions, remind when to reorder

### Recovery
- **Recovery score** — composite daily metric from sleep quality, HRV (if available), session load, and self-reported soreness
- **Sleep quality logger** — free-text nightly log converted to structured data; trend analysis over weeks
- **Injury tracker** — log nagging issues, track duration and severity trend, alert if something's been logged for too long without resolution
- **Mobility deficit flag** — based on session notes mentioning stiffness/tightness, build targeted mobility routine

### Performance Metrics
- **PR tracker** — log and chart strength PRs (lift, bodyweight benchmarks, conditioning tests)
- **Monthly performance review** — auto-generated summary: volume trends, PRs set, weight trend, recovery patterns, key sessions
- **Readiness briefing** — morning check-in: today's training recommendation based on yesterday's load and sleep

---

## Periodization Awareness

Agent understands these phases and adjusts recommendations accordingly:
- **Off-season** (base building, higher volume)
- **Pre-camp** (sport-specific ramp-up)
- **Fight camp** (peak intensity, lower volume, sharpen skills)
- **Taper** (2 weeks out — preserve sharpness, shed fatigue)
- **Recovery week** (post-fight or post-camp deload)
