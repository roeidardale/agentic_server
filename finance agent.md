# Finance Agent
*Portfolio tracking, crypto, budgeting, tax prep, and opportunity detection*

More detailed and active than the finance slice in Lifestyle Agent. Lifestyle handles day-to-day expenses; this agent handles wealth building and strategy.

---

## Tools

| Tool | Why |
|---|---|
| Bank export parser (CSV/OFX) | Parse statements for transaction categorization |
| CoinGecko / CoinMarketCap API | Crypto prices, portfolio valuation, alerts |
| Yahoo Finance / Alpha Vantage API | Stock/ETF prices, fundamentals |
| Tax calculator (local rules) | Estimate capital gains liability |
| Web search + fetch | Research assets, read earnings reports, macro news |
| Note writer | Store portfolio snapshots, decisions log |
| Notification channel | Price alerts, opportunity signals, monthly reports |
| Spreadsheet/CSV writer | Export reports, tax docs |

---

## Skills

### Portfolio Tracking
- **Net worth snapshot** — aggregate all assets (cash, crypto, stocks, other) into a single number; track over time
- **Portfolio valuation** — daily or on-demand valuation of holdings with P&L breakdown
- **Allocation drift check** — compare current allocation vs target allocation; flag when rebalance is needed
- **Performance benchmarking** — compare your returns vs BTC, ETH, S&P500, or any custom benchmark

### Crypto
- **DCA tracker** — log recurring buys, compute average cost basis, track gain/loss vs current price
- **On-chain alert monitor** — large wallet movements, exchange inflows (macro signal for volatility)
- **Staking/yield tracker** — log staking rewards, compute effective APY, track compound growth
- **Gas fee optimizer** — suggest low-fee windows for on-chain transactions (ETH/L2 focused)
- **New opportunity radar** — surface trending protocols, new L2s, or yield opportunities with risk rating

### Stocks & ETFs
- **Watchlist screener** — daily scan of watchlist for technical signals (breakouts, volume spikes, earnings upcoming)
- **Earnings calendar** — track upcoming earnings for holdings and watchlist; brief pre-earnings summary
- **Fundamental snapshot** — P/E, revenue growth, debt levels for any ticker on demand
- **Macro briefing** — weekly summary of macro events (Fed, inflation data, job reports) and likely market impact

### Budgeting & Expenses
- **Monthly budget vs actual** — compare spending to targets by category; flag overruns
- **Expense anomaly detection** — surface unusual charges or spending pattern changes
- **Subscription audit** — list all recurring charges, flag unused ones, track MoM change
- **Savings rate tracker** — compute monthly savings rate and trend

### Tax & Planning
- **Capital gains estimate** — given trades this year, estimate tax liability (short-term vs long-term)
- **Tax-loss harvesting scan** — identify positions with unrealized losses that could offset gains
- **Year-end tax summary** — generate structured summary of all taxable events for filing

### Decisions Log
Every financial decision gets a log entry: date, asset, action, reasoning, expected outcome. Reviewed monthly to learn from what worked vs what didn't.
