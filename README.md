# 🔍 ScoutINNtelligence (Scout) — Dual-Intelligence Lead Generation Platform

![Python](https://img.shields.io/badge/Python-3.11+-blue?style=flat-square&logo=python)
![Next.js](https://img.shields.io/badge/Next.js-15-black?style=flat-square&logo=next.js)
![FastAPI](https://img.shields.io/badge/FastAPI-Latest-009688?style=flat-square&logo=fastapi)
![LLM](https://img.shields.io/badge/LLM-Groq-green?style=flat-square)
![Storage](https://img.shields.io/badge/Storage-JSON%20%2F%20CSV-lightgrey?style=flat-square)
![Tests](https://img.shields.io/badge/Tests-78%20pytest-0a9edc?style=flat-square&logo=pytest)
![Search](https://img.shields.io/badge/Search-Tavily%20%2B%20SerpAPI-orange?style=flat-square)
![Deployed](https://img.shields.io/badge/Deployed-Vercel%20%2B%20Railway-000000?style=flat-square)
![Status](https://img.shields.io/badge/Status-Deployed-success?style=flat-square)

> **Finds the startups worth pursuing and the buyers ready to buy, ranked and backed by cited evidence, in minutes instead of days.**
>
> | | |
> |---|---|
> | **For** | B2B sales and growth teams |
> | **Input** | Your target criteria (Supply Scan) or a list of companies (Demand Scan) |
> | **Output** | Tiered startup rankings and sales-ready leads with source-cited signals |
> | **Core tech** | FastAPI, Next.js 15 + React 19, Groq (gpt-oss-120b) + Claude Haiku, Tavily / SerpAPI search, Firecrawl / Playwright, deployed on Vercel + Railway |

---

## 🚀 What is ScoutINNtelligence?

**ScoutINNtelligence** (internally **Scout**) is an **enterprise lead generation intelligence platform** that uses dual scanning to identify high-potential targets:

1. 🔎 **Supply Scan** — discover & rank startups matching your criteria
2. 👥 **Demand Scan** — identify potential clients with buying intent signals

### 💡 The Core Problem It Solves:

> **Sales teams spend hours researching prospects.** Scout automates the discovery, qualification, and intent validation in minutes.

---

## 🎯 Problem Statement

### The Challenge 📊

Traditional B2B prospecting is broken:

- ❌ **Manual research is slow** — finding 50 prospects takes a day
- ❌ **Lists are outdated** — intent signals are missed or stale
- ❌ **No qualification framework** — every prospect seems equal
- ❌ **Search results are noisy** — 80% of results are irrelevant
- ❌ **Funding data is incomplete** — missing growth signals
- ❌ **No intent tracking** — can't spot when companies are ready to buy

### The Solution ✨

Scout solves prospecting in two directions:

**📈 Supply Side** — Find startups in growth mode (new funding, expansion, hiring)
**📥 Demand Side** — Find buyers with proven intent (needs + capacity + triggers)

Both pipelines use intelligent ranking, so sales teams focus on the highest-potential targets first.

---

## ✨ Key Features

### 1️⃣ **Supply Scan — Startup Discovery & Ranking** 🚀

**What it does:**
- 🔍 Searches for startups matching your criteria (industry, funding stage, location)
- 🧠 Uses LLM to analyze company websites and extract structured data
- 🏆 Scores each startup 0–100 on a 7-criterion weighted rubric (configurable in YAML)
- 📊 Bands: **Strategic Partnership Target** (80+), **Explore / Pilot** (65+), **Interesting but non-core**
- ⚠️ Flags duplicates, non-companies, and irrelevant results

**Example Output:**
```
✨ Strategic Partnership Target (Score 87)
Company: TechVentures Inc
Founding: 2021 | Funding: Series A | Team Size: 45
Location: San Francisco, CA
Match: SaaS platform + strong team + proven funding
```

### 2️⃣ **Demand Scan — Client Qualification** 💼

**What it does:**
- 📋 Takes user-provided company list
- 🔎 Searches for **three types of signals**:
  - **MarTech Need** (2+ signals in 12 months) — what problems they're solving
  - **Buying Capacity** (2+ current signals) — do they have budget/team?
  - **Actionability** (1+ trigger in 18 months) — are they ready to buy?
- ✅ Only surfaces companies meeting ALL THREE filters
- 📊 Provides evidence for each signal (with source + quote)
- 🎯 Ranks by signal confidence and recency

**Example Output:**
```
✅ QUALIFIED LEAD
Company: RetailBrand Co
MarTech Need: ✅ (3 signals)
  • Loyalty program launch (Jan 2026)
  • Omnichannel strategy initiative (Dec 2023)
  • First-party data CDP implementation (Mar 2026)

Buying Capacity: ✅ (2 signals)
  • CMO hired (Sep 2026)
  • Enterprise MarTech stack (Salesforce + Adobe)

Actionability: ✅ (1 trigger)
  • Digital transformation announcement (Feb 2026)

Status: SALES READY 🎯
```

### 3️⃣ **Multi-Source Intelligence Gathering** 🌐

- ✅ **Primary sources:**
  - Company websites (official facts)
  - LinkedIn company pages (team, hiring signals)
  - Press releases (announcements, expansion)
  - Annual reports (strategy, financials)

- ✅ **Industry sources:**
  - Trade publications (sector-specific news)
  - Funding databases (Crunchbase, Tracxn)
  - Job boards (hiring velocity)
  - News aggregators (breaking moves)

- ✅ **Smart fallbacks:**
  - Tavily + SerpAPI for comprehensive search
  - DuckDuckGo as backup when primary sources fail
  - Firecrawl + Playwright for difficult websites

### 4️⃣ **Historical Tracking & Snapshots** 📚

- ✅ Every scan creates a timestamped snapshot
- ✅ Compare leads across scans (see progress)
- ✅ Track when companies first appeared
- ✅ Identify "hot" companies (multiple scans = sustained growth)
- ✅ Export results as CSV or JSON

### 5️⃣ **Configurable Rules Engine** ⚙️

- ✅ Define your own supply criteria (industry, team size, funding)
- ✅ Set demand signal thresholds (time windows, minimum counts)
- ✅ Customize trusted sources (which publications matter to you)
- ✅ Adjust exclusion rules (blocked companies, blocked domains)
- ✅ YAML-based configuration (no code changes needed)

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│              VERCEL FRONTEND (Next.js + React)               │
│    Dashboard │ Supply Scan │ Demand Scan │ Insights        │
│                (Streamed Progress, CSV/JSON Export)          │
└────────────────────────┬────────────────────────────────────┘
                         │ REST API
                         ▼
┌─────────────────────────────────────────────────────────────┐
│              RAILWAY BACKEND (FastAPI + Python)              │
│  ┌──────────────────────────────────────────────────────────┐│
│  │           Supply Pipeline                                 ││
│  │  Search → Filter → Website Read → LLM Extract → Score   ││
│  │                                                           ││
│  │           Demand Pipeline                                 ││
│  │  Companies → Search Evidence → LLM Signal Detection     ││
│  │           → Filter (3-step) → Qualify → Rank            ││
│  └──────────────────────────────────────────────────────────┘│
│           ▲                              ▲
│    ┌──────┴──────────────┬──────────────┴──────┐
│    │                     │                      │
│    ▼                     ▼                      ▼
│ ┌─────────────┐   ┌────────────┐      ┌──────────────┐
│ │ Tavily API  │   │ SerpAPI    │      │ Groq LLM     │
│ │(Search +    │   │(Web Search)│      │(Extraction + │
│ │ Extraction) │   │            │      │ Classification)
│ └─────────────┘   └────────────┘      └──────────────┘
│
│  Firecrawl (web crawling) | Playwright (complex pages)
│
│  ┌──────────────────────────────────────────────────────────┐
│  │       STORAGE (JSON / CSV on a Railway volume)           │
│  │  results · demand_results · runs/<timestamp> snapshots   │
│  │  excluded · seen.json (dedup) · insights · errors.log    │
│  └──────────────────────────────────────────────────────────┘
└─────────────────────────────────────────────────────────────┘
```

---

## 🔄 Workflow

### Supply Scan Pipeline 🚀

```
1️⃣ LOAD RULES
   Load criteria.yaml → market definition
   Load filters.yaml → exclusion rules
        ↓
2️⃣ SEARCH
   Build search queries from criteria
   Tavily + SerpAPI (parallel, merged results)
   Fallback: DuckDuckGo
        ↓
3️⃣ FILTER BAD RESULTS
   Remove: roundup articles, glossaries, job pages
   Remove: blocked domains, non-companies
   Remove: duplicates (URL normalization)
        ↓
4️⃣ FIND OFFICIAL WEBSITE
   If search result = news article:
      → Search for company official website
      → Validate domain matches company name
        ↓
5️⃣ READ WEBSITE
   Chain:
   1. Firecrawl (preferred)
   2. Tavily extraction (fallback)
   3. Direct request + text cleanup
   4. Playwright (JavaScript-heavy sites)
        ↓
6️⃣ EXTRACT WITH LLM
   Send clean text to Groq (gpt-oss-120b); Claude Haiku judges the
   judgment-sensitive steps (vertical match, hard-exclusion evidence)
   Extract: founders, funding stage, market, product
        ↓
7️⃣ APPLY BUSINESS RULES
   Score: 7-criterion weighted rubric (criteria.yaml), 0–100
   Band: Strategic Partnership Target (80+) | Explore / Pilot (65+) | Interesting but non-core
   Add flags: ⚠️ incomplete data, 🚩 warning
        ↓
8️⃣ OPTIONAL FUNDING LOOKUP
   For promising candidates: search funding details
   Aggregate: total raised, stage, recent investors
        ↓
9️⃣ SAVE RESULTS
   data/results.csv (latest)
   data/results.json (structured)
   data/excluded.csv (what was filtered out)
   data/runs/<timestamp>/ (permanent snapshot)
   data/seen.json (all-time list for dedup)
        ↓
🔟 SHOW PROGRESS
   Website receives progress updates (streaming)
   Displays: search results → analysis → final scores
```

### Demand Scan Pipeline 👥

```
1️⃣ USER INPUT
   Company name + optional domain
        ↓
2️⃣ LOAD DEMAND RULES
   Load demand_criteria.yaml:
   • 9 MarTech Need signals (last 12 months)
   • 9 Buying Capacity signals (current)
   • 9 Actionability triggers (last 18 months)
        ↓
3️⃣ SEARCH FOR EVIDENCE PAGES
   Build candidate pages:
   • Official: /newsroom, /press-release, /investors
   • LinkedIn: company page + jobs page
   • Publications: trade/industry/funding sites
        ↓
4️⃣ READ PAGES
   Same chain as Supply Scan:
   Firecrawl → Tavily → Direct → Playwright
        ↓
5️⃣ EXTRACT SIGNALS WITH LLM
   Groq receives page + 27-signal catalog
   Groq reports:
   • Which signal detected (name)
   • Evidence quote
   • Date (if available)
   └─ Groq does NOT make pass/fail decision
        ↓
6️⃣ COMBINE EVIDENCE
   Merge across all pages per company
   Source priority:
   1. Official company sources (highest)
   2. Trade publications
   3. Funding databases
   4. News/other (lowest)
   └─ Keep supporting evidence even if lower priority
        ↓
7️⃣ APPLY THREE FILTERS
   
   FILTER 1: MarTech Need
   Count signals from last 12 months
   ≥ 2 signals? → PASS
   
   FILTER 2: Buying Capacity
   Count TRUE current signals
   ≥ 2 true? → PASS
   
   FILTER 3: Actionability
   Count triggers from last 18 months
   ≥ 1 trigger? → PASS
   
   ALL THREE PASS? → QUALIFIED LEAD ✅
        ↓
8️⃣ RANK QUALIFIED LEADS
   By: signal recency, trigger strength, capacity signals
        ↓
9️⃣ SAVE RESULTS
   data/demand_results.json (latest)
   data/demand_runs/<timestamp>/results.json (snapshot)
   Error log for failed pages/companies
        ↓
🔟 DISPLAY TO USER
   Website shows:
   • Qualified leads (sales-ready)
   • Signal breakdown per company
   • Evidence quotes + sources
   • Previous scan history
```

### Insights Workflow 📰

```
1️⃣ USER REFRESHES INSIGHTS
        ↓
2️⃣ FETCH ARTICLES
   Collect from configured sources:
   • Industry publications
   • Tech news
   • Trade journals
   • Company announcements
        ↓
3️⃣ DEDUPLICATE
   Remove duplicate articles (content + domain)
        ↓
4️⃣ LOAD CONTEXT
   Your company profile from criteria.yaml
   (industry, markets, keywords, interests)
        ↓
5️⃣ ASK GROQ
   "Is this article relevant to our company?
    Why does it matter?"
        ↓
6️⃣ SAVE & DISPLAY
   Save to data/insights.json
   Website displays ranked by relevance
```

---

## 📊 Sample Outputs

*Illustrative output. Company names are fictional.*

### Supply Scan Results

```
🔍 SUPPLY SCAN COMPLETED
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📊 Summary:
  ✅ 127 companies found
  🏆 Strategic Partnership Target: 8 companies
  📈 Explore / Pilot: 34 companies
  📋 Interesting but non-core: 52 companies
  ❌ Excluded: 33 (duplicates, non-companies, blocked domains)

🎯 Top 3 Results:

1. CloudScale Systems
   Score: 92 | Founded: 2020 | Team: 67
   Funding: Series B ($15M) | Location: Austin, TX
   Match: Cloud infrastructure + strong VC backing + enterprise customers
   
2. DataPulse Analytics
   Score: 89 | Founded: 2019 | Team: 43
   Funding: Series A ($8M) | Location: San Francisco, CA
   Match: Analytics platform + profitable metrics + growing user base
   
3. NextGen Commerce
   Score: 87 | Founded: 2021 | Team: 52
   Funding: Series A ($12M) | Location: London, UK
   Match: E-commerce tools + international expansion + strong partnerships
```

### Demand Scan Results

```
👥 DEMAND SCAN COMPLETED
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📊 Summary:
  Companies Analyzed: 24
  ✅ Qualified Leads: 6
  📋 Partial Match: 8
  ❌ Not Qualified: 10

🎯 QUALIFIED LEADS (Sales-Ready):

1. RetailCorp International
   ✅ MarTech Need (3/9 signals)
      • Loyalty program launch (Mar 2026)
      • Omnichannel strategy initiative (Feb 2026)
      • First-party data CDP implementation (Jan 2026)
   
   ✅ Buying Capacity (2/9 signals)
      • Chief Marketing Officer hired (Sep 2026)
      • Salesforce + Adobe MarTech stack
   
   ✅ Actionability (1/9 triggers)
      • Digital transformation announcement (Feb 2026)
   
   Status: 🎯 SALES READY

2. Fashion Brands Ltd
   ✅ MarTech Need (4/9 signals)
      • D2C channel expansion (Apr 2026)
      • Customer personalization initiative (Mar 2026)
      • Mobile app relaunch (Feb 2026)
      • CRM transformation project (Dec 2023)
   
   ✅ Buying Capacity (3/9 signals)
      • CMO + Digital Head on team
      • In-house MarTech team (5+ roles hiring)
      • Series B funding ($20M) received (Jun 2026)
   
   ✅ Actionability (2/9 triggers)
      • New CEO (Mar 2026)
      • Geographic expansion (Apr 2026)
   
   Status: 🎯 PRIORITY LEAD
```

---

## 🛠️ Tech Stack

### 🎨 Frontend — Vercel + Next.js

| Technology | Purpose |
|-----------|---------|
| **Next.js 15** (App Router) | Application framework |
| **React 19** | UI components |
| **TypeScript 5** | Type safety |
| **Tailwind CSS 4** | Styling |
| **Vercel** | Deployment |

**Features:** streamed scan progress · tables and charts · CSV/JSON export · eight pages (Dashboard, Startups, Run Scan, Demand Scan, Insights, Exclusions, Reports, Settings)

### 🔧 Backend — Railway + FastAPI

| Technology | Purpose |
|-----------|---------|
| **FastAPI + Uvicorn** | REST API, streamed (SSE) scan progress |
| **Python 3.10+** | Pipeline logic, LLM and search integration |
| **Railway** (Nixpacks) | Backend deployment with a persistent volume |
| **pytest** | 78 tests across 9 files |

### 💾 Storage — Files on a Railway Volume

Scan results, run snapshots, exclusions, insights and run history are stored as JSON/CSV under `data/`, mounted on a Railway volume in production (`SCOUT_DATA_DIR`). Each run also writes a timestamped snapshot, and `seen.json` de-duplicates companies across runs. File storage keeps the deployment simple; a database is the planned step if multi-user history is needed.

### 🔍 Search & Scraping

| Service | Purpose |
|---------|---------|
| **Tavily** | Web search + page extraction |
| **SerpAPI** | Google search results (parallel) |
| **DuckDuckGo** | Free fallback (no key required) |
| **Firecrawl** | Intelligent web scraping |
| **Playwright** | Headless browser for JavaScript-heavy sites |

**Search strategy:** run Tavily + SerpAPI in parallel → merge and de-duplicate → fall back to DuckDuckGo if both fail → a search failure never stops a scan.

### 🤖 LLMs

| Model | Used for |
|-------|----------|
| **Groq `openai/gpt-oss-120b`** | Default: field extraction, demand-signal detection (JSON mode) |
| **Claude Haiku 4.5** | Judgment-sensitive stages: vertical matching and hard-exclusion evidence |
| **NVIDIA NIM** (fallback) | Intermediate fallback for the Claude-routed stages |

Models and per-stage routing are set in `config/settings.yaml`, so swapping a model is a config change, not a code change.

---

## 🚀 Deployment & Setup

### Local Development 💻

```bash
cd supply_agent
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
playwright install chromium          # for JavaScript-heavy sites

cp .env.example .env                 # add your keys (see below)
(cd web && npm install)              # Node 20.9+ required

./run_dev.sh                         # API on :8000, frontend on :3000
# API docs: http://localhost:8000/docs
```

### Production 🌐

- **Backend → Railway** (`railway.toml`, Nixpacks): `uvicorn api.main:app`; mount a volume at `/data` and set `SCOUT_DATA_DIR=/data`
- **Frontend → Vercel** (`web/`, Next.js preset); point it at the backend with `NEXT_PUBLIC_API_URL`

---

## ⚙️ Configuration

All business rules live in YAML. Changing scoring, thresholds or exclusions needs no Python changes.

| File | Controls |
|------|----------|
| `config/criteria.yaml` | Scoring weights, score bands, hard exclusions, verticals, funding-stage weights, source pool |
| `config/demand_criteria.yaml` | The 27 demand signals (9 per filter), thresholds, time windows, trusted sources |
| `config/filters.yaml` | Company blacklist, blocked/news domains, aliases, resolver confidence threshold |
| `config/settings.yaml` | LLM provider/model, per-stage routing, concurrency, timeouts, output paths |

**Supply scoring rubric** (weights sum to 100):

```yaml
criteria_weights:
  solves_operating_problem: 20
  marketing_unification_impact: 20
  strengthens_core_vertical: 15
  revenue_potential: 15
  tech_led_differentiation: 15
  mobility_dna_relevance: 10
  cross_category_scalability: 5

score_bands:
  - {min: 80, label: "Strategic Partnership Target"}
  - {min: 65, label: "Explore / Pilot"}
  - {min: 0,  label: "Interesting but non-core"}
```

**Demand thresholds** (all three must pass):

```yaml
thresholds:
  martech_need:    {min_signals: 2, window_months: 12}
  buying_capacity: {min_signals: 2}                      # current evidence, no window
  actionability:   {min_signals: 1, window_months: 18}
```

### Environment Variables

```env
GROQ_API_KEY=...        # default LLM
CLAUDE_API_KEY=...      # judgment-sensitive stages
NVIDIA_API_KEY=...      # NIM fallback
TAVILY_API_KEY=...
SERP_API_KEY=...
FIRECRAWL_API_KEY=...
SCOUT_DATA_DIR=/data    # production: persistent volume path
NEXT_PUBLIC_API_URL=... # frontend → backend URL
FRONTEND_ORIGINS=...    # extra CORS origins (comma-separated)
```

---

## 📱 UI Pages

| Page | What it does |
|------|--------------|
| **Dashboard** | Overview of recent scans and results |
| **Run Scan** | Start a Supply Scan and watch streamed progress |
| **Startups** | Ranked startups with score, band and per-criterion breakdown; CSV/JSON export |
| **Demand Scan** | Add companies (or auto-discover), stream progress, review qualified leads with evidence quotes, sources and dates; browse past scans |
| **Insights** | MarTech news feed ranked by relevance to your company profile |
| **Exclusions** | Everything filtered out, and why |
| **Reports** | Run history and exports |
| **Settings** | Read-only view of the active configuration |

---

## 🛡️ Reliability & Performance

### Security
- 🔑 API keys live in environment variables, never in code or config
- 🛡️ Typed request validation (FastAPI / Pydantic)
- 🌐 CORS restricted to configured frontend origins

### Performance
- 🚀 Tavily + SerpAPI queried in parallel; candidates processed concurrently (`max_parallel_candidates`)
- 📡 Scan progress streamed to the UI (Server-Sent Events)
- ⏱️ Timeouts on external calls

### Error Handling
- ✅ Failed search → fallback to DuckDuckGo
- ✅ Failed page → next scraper in the chain (Firecrawl → Tavily → direct → Playwright), then skip
- ✅ Failed LLM call → logged and routed to the fallback model where configured
- ✅ Failed company → error recorded, scan continues
- ✅ All errors logged to `data/errors.log`

---

## 💰 Cost Optimization

- **De-duplication:** `seen.json` stops the same company or domain being re-processed across runs
- **Free fallback:** DuckDuckGo covers search when paid providers fail
- **Right-sized models:** high-volume extraction on Groq's gpt-oss-120b; Claude Haiku only for the two judgment-sensitive stages
- **Prompt caching:** the Claude calls use a cacheable prompt prefix
- **Bounded crawling:** `max_pages_per_company` caps pages read per company

---

## 📈 Design Principles

### 1️⃣ **Evidence-Based Ranking** 📊
- Every score is justifiable (a weighted, per-criterion rubric)
- Every signal has a source (with quote + date)
- Every lead must pass ALL three filters (no fuzzy logic)

### 2️⃣ **Resilience Over Perfection** 🛡️
- One failed search → fallback to another
- One failed page → skip and continue
- One bad source → keep supporting evidence
- Never stop a scan due to one failure

### 3️⃣ **Transparency in Filtering** 👁️
- Show excluded companies (and why)
- Show partial matches (which filter failed)
- Show evidence sources (so you can verify)

### 4️⃣ **Configuration Over Code** ⚙️
- Business rules in YAML (no Python changes)
- Settings versionable and auditable

### 5️⃣ **Time-Based Decision Making** ⏱️
- MarTech Need: last 12 months (recent trends)
- Actionability: last 18 months (ready-to-buy window)
- Signal dating: capture and validate dates

---

## 🧪 Testing

```bash
cd supply_agent
pytest        # 78 tests across 9 files
```

Covers API endpoints, provider workflow and fallbacks, official-website resolution, V3 scouting validation, demand auto-discovery, insights pipeline and workload limits.

---

## 📁 Project Structure

```text
Scout_Agent/
└── supply_agent/
    ├── api/
    │   ├── main.py              # FastAPI app: supply, insights, exports, settings
    │   └── demand_main.py       # Demand Scan routes (SSE streaming)
    ├── pipeline/
    │   ├── discovery.py         # Search → candidate companies
    │   ├── exclude.py           # Two-pass exclusion rules
    │   ├── resolve.py           # Find the official website
    │   ├── scrape.py            # Firecrawl → Tavily → direct → Playwright
    │   ├── scoring.py           # LLM extraction + weighted rubric
    │   ├── ranking.py           # Sort, band, dedup, write outputs
    │   ├── funding_lookup.py    # Optional funding search
    │   ├── pipeline_runner.py   # Supply orchestration
    │   └── demand/              # Demand Scan pipeline
    ├── utils/                   # LLM client, search providers, insights, run history
    ├── config/                  # criteria · demand_criteria · filters · settings (YAML)
    ├── web/                     # Next.js 15 frontend (src/app, components, lib)
    ├── tests/                   # pytest suite
    ├── data/                    # results, runs/, demand_runs/, errors.log
    ├── railway.toml
    └── run_dev.sh
```

---

## 🎯 API Endpoints

```
GET  /api/health                       Service status
GET  /api/dashboard                    Overview metrics
GET  /api/scopes                       Available scan scopes
GET  /api/diagnostics                  Run diagnostics

POST /api/scan                         Start a Supply Scan (streamed)
GET  /api/scan/stages                  Pipeline stages
GET  /api/startups                     Ranked startups
GET  /api/startups/{name}              One startup in detail
GET  /api/exclusions                   Filtered-out companies
GET  /api/reports                      Run history
GET  /api/exports/results.csv|.json    Export results
GET  /api/exports/excluded.csv         Export exclusions

POST /api/demand/scan                  Demand Scan for given companies (streamed)
POST /api/demand/auto-scan             Demand Scan with auto-discovery (streamed)
GET  /api/demand/leads                 Qualified leads
GET  /api/demand/history               Past demand scans
GET  /api/demand/criteria              Active criteria
GET  /api/demand/scan/stages           Pipeline stages

GET  /api/insights                     Latest insights
POST /api/insights/refresh             Fetch new articles (background job)
GET  /api/insights/refresh/{job_id}    Job status

GET  /api/settings                     Active configuration (read-only)
```

---

## 🚀 Future Roadmap

### Phase 2 (Q4 2026)
- 🗄️ **Database storage** — move from files to Postgres for multi-user history
- 🤖 **AI-powered outreach templates** — generate emails per company
- 📞 **CRM integration** — sync leads to Salesforce/HubSpot
- 🔔 **Alert system** — notify when new high-quality leads appear

### Phase 3 (2027)
- 🌍 **International expansion** — support multiple countries
- 📱 **Mobile app** — iOS/Android native apps
- 🎬 **Video intelligence** — analyze founder/CEO videos
- 🤝 **Collaboration features** — team notes, deal tracking

---

## 🆘 Troubleshooting

### ❌ Supply scan collects nothing
- Check `TAVILY_API_KEY` and `SERP_API_KEY` validity
- Check `criteria.yaml` (too strict filters?)
- Check `filters.yaml` (blocking too much?)
- See `data/errors.log` for details

### ❌ Demand scan finds no qualified leads
- Verify company domains are correct
- Check if 12-month/18-month windows are right for your market
- Review signal evidence (maybe they're weak signals)
- See `data/errors.log` for what failed

### ❌ Website fails to load
- Check `NEXT_PUBLIC_API_URL` points to backend
- Check backend is running (`http://localhost:8000/docs`)
- Check database connection in logs

### ❌ LLM extraction fails
- Check `GROQ_API_KEY` validity
- Check if you're hitting rate limits
- Failed extractions logged to `data/errors.log`

---

## 📜 License

**Proprietary** — Enterprise lead generation platform.

---

## 📊 Metrics & Stats

| Metric | Value |
|--------|-------|
| **Automated tests** | 78 (pytest, 9 files) |
| **Demand signals evaluated** | 27 (9 MarTech Need · 9 Buying Capacity · 9 Actionability) |
| **Frontend pages** | 8 |
| **REST endpoints** | 20+ |
| **Search / scrape providers with fallback** | 5 |
| **Supply scoring criteria** | 7 (weights sum to 100) |

---

## 🎉 Built With ❤️

**Frontend:** Next.js + React + Vercel  
**Backend:** FastAPI + Python + Railway  
**Data:** JSON / CSV on a Railway volume  
**Search:** Tavily + SerpAPI + DuckDuckGo  
**Scraping:** Firecrawl + Playwright  
**LLM:** Groq (gpt-oss-120b) + Claude Haiku 4.5

---

**Last Updated:** September 2026  
**Version:** 2.0
