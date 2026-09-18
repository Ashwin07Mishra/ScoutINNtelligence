# 🔍 Scout — Dual-Intelligence Lead Generation Platform

![Python](https://img.shields.io/badge/Python-3.11+-blue?style=flat-square&logo=python)
![Next.js](https://img.shields.io/badge/Next.js-14-black?style=flat-square&logo=next.js)
![FastAPI](https://img.shields.io/badge/FastAPI-Latest-009688?style=flat-square&logo=fastapi)
![LLM](https://img.shields.io/badge/LLM-Groq-green?style=flat-square)
![Database](https://img.shields.io/badge/Database-Supabase-3ecf8e?style=flat-square&logo=supabase)
![Search](https://img.shields.io/badge/Search-Tavily%20%2B%20SerpAPI-orange?style=flat-square)
![Deployed](https://img.shields.io/badge/Deployed-Vercel%20%2B%20Railway-000000?style=flat-square)
![Status](https://img.shields.io/badge/Status-Production-success?style=flat-square)

---

## 🚀 What is Scout?

**Scout** is an **enterprise lead generation intelligence platform** that uses dual scanning to identify high-potential targets:

1. 🔎 **Supply Scan** — discover & rank startups matching your criteria
2. 👥 **Demand Scan** — identify potential clients with buying intent signals

### 💡 The Core Problem It Solves:

> **Sales teams spend hours researching prospects.** Scout automates the discovery, qualification, and intent validation in minutes.

![Image #1: Scout Dashboard]

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
- 🏆 Ranks by relevance score (0–100)
- 📊 Classifies as: Tier 1 (high-fit), Tier 2 (medium-fit), Tier 3 (exploratory)
- ⚠️ Flags duplicates, non-companies, and irrelevant results

**Example Output:**
```
✨ Tier 1 (Score 87)
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
  • Loyalty program launch (Jan 2024)
  • Omnichannel strategy initiative (Dec 2023)
  • First-party data CDP implementation (Mar 2024)

Buying Capacity: ✅ (2 signals)
  • CMO hired (Sep 2024)
  • Enterprise MarTech stack (Salesforce + Adobe)

Actionability: ✅ (1 trigger)
  • Digital transformation announcement (Feb 2024)

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

![Image #2: Scout Architecture]

```
┌─────────────────────────────────────────────────────────────┐
│              VERCEL FRONTEND (Next.js + React)               │
│    Dashboard │ Supply Scan │ Demand Scan │ Insights        │
│                   (Real-time Progress, Export)               │
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
│  │         DATABASE (Supabase PostgreSQL)                   │
│  │  startup_results | demand_results | scan_history        │
│  │  excluded_companies | signal_evidence                    │
│  └──────────────────────────────────────────────────────────┘
│
│  ┌──────────────────────────────────────────────────────────┐
│  │              CACHE (Redis)                               │
│  │  website_cache | search_results | scan_snapshots        │
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
   Send clean text to Groq (gpt-oss-120b)
   Extract: founders, funding stage, market, product
        ↓
7️⃣ APPLY BUSINESS RULES
   Score: (team_quality × 0.3) + (market_fit × 0.4) + (funding × 0.3)
   Classify: Tier 1 (85+) | Tier 2 (60-84) | Tier 3 (40-59)
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

![Image #3: Data Flow Diagram]

---

## 📊 Sample Outputs

### Supply Scan Results

```
🔍 SUPPLY SCAN COMPLETED
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📊 Summary:
  ✅ 127 companies found
  🏆 Tier 1: 8 companies (high-fit)
  📈 Tier 2: 34 companies (medium-fit)
  📋 Tier 3: 52 companies (exploratory)
  ❌ Excluded: 33 (duplicates, non-companies, blocked domains)

🎯 Top 3 Tier 1 Results:

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
      • Loyalty program launch (Mar 2024)
      • Omnichannel strategy initiative (Feb 2024)
      • First-party data CDP implementation (Jan 2024)
   
   ✅ Buying Capacity (2/9 signals)
      • Chief Marketing Officer hired (Sep 2024)
      • Salesforce + Adobe MarTech stack
   
   ✅ Actionability (1/9 triggers)
      • Digital transformation announcement (Feb 2024)
   
   Status: 🎯 SALES READY
   Score: 8.5/10
   Recommended Action: Outreach to CMO

2. Fashion Brands Ltd
   ✅ MarTech Need (4/9 signals)
      • D2C channel expansion (Apr 2024)
      • Customer personalization initiative (Mar 2024)
      • Mobile app relaunch (Feb 2024)
      • CRM transformation project (Dec 2023)
   
   ✅ Buying Capacity (3/9 signals)
      • CMO + Digital Head on team
      • In-house MarTech team (5+ roles hiring)
      • Series B funding ($20M) received (Jun 2024)
   
   ✅ Actionability (2/9 triggers)
      • New CEO (Mar 2024)
      • Geographic expansion (Apr 2024)
   
   Status: 🎯 PRIORITY LEAD
   Score: 9.2/10
   Recommended Action: Executive briefing
```

---

## 🛠️ Tech Stack

### 🎨 Frontend — Vercel + Next.js

| Technology | Purpose | Version |
|-----------|---------|---------|
| **Next.js 14** | Full-stack framework, SSR, API routes | Latest |
| **React 18** | Component library, hooks | Latest |
| **Vercel** | Deployment, CDN, edge functions | – |
| **TypeScript** | Type safety | 5.x |
| **TailwindCSS** | Styling | Latest |
| **SWR / React Query** | Data fetching, caching | Latest |

**Features:**
- 📊 Real-time scan progress (WebSocket)
- 📈 Data visualization (charts, tables)
- 🔄 Export to CSV/JSON
- 📱 Responsive design
- 🌙 Dark mode

### 🔧 Backend — Railway + FastAPI

| Technology | Purpose | Version |
|-----------|---------|---------|
| **FastAPI** | REST API, async, streaming | Latest |
| **Python** | Core logic, LLM/search integration | 3.11+ |
| **Railway** | Containerized deployment | – |
| **Uvicorn** | ASGI server | Latest |
| **Pydantic** | Schema validation | 2.x |

**Key Modules:**
```
backend/
├── api/
│   ├── main.py                # FastAPI app
│   ├── supply_main.py         # Supply Scan routes
│   └── demand_main.py         # Demand Scan routes
├── pipeline/
│   ├── pipeline_runner.py     # Supply orchestration
│   ├── demand/
│   │   └── runner.py          # Demand orchestration
│   ├── stages/
│   │   ├── search.py
│   │   ├── filter.py
│   │   ├── scrape.py          # Website reading
│   │   └── extract.py         # LLM extraction
│   └── scoring.py             # Ranking logic
├── utils/
│   ├── search_provider.py     # Tavily + SerpAPI + DuckDuckGo
│   ├── web_scraper.py         # Firecrawl + Playwright
│   ├── llm_client.py          # Groq integration
│   └── dedup.py               # Duplicate detection
├── config/
│   ├── criteria.yaml          # Supply rules
│   ├── demand_criteria.yaml   # Demand rules
│   ├── filters.yaml           # Exclusions
│   └── settings.yaml          # Technical config
└── db/
    ├── models.py              # SQLAlchemy ORM
    └── connection.py          # Supabase
```

### 💾 Database — Supabase (PostgreSQL)

| Table | Purpose |
|-------|---------|
| `startup_results` | Supply scan results (companies, scores, tiers) |
| `demand_results` | Qualified leads (signals, sources, dates) |
| `signal_evidence` | Detailed evidence per signal (quotes, sources) |
| `scan_history` | Metadata for each scan run (timestamp, summary) |
| `excluded_companies` | What was filtered out (why, when) |
| `seen_domains` | All-time domain list (dedup across scans) |

**Features Used:**
- ✅ PostgREST API (auto-endpoints)
- ✅ Row-level security (RLS)
- ✅ Full-text search (on company names)
- ✅ JSON columns (flexible signal storage)

### 🔍 Search & Scraping

| Service | Purpose | Config |
|---------|---------|--------|
| **Tavily** | Web search + page extraction | api_key |
| **SerpAPI** | Google search results (parallel) | api_key |
| **DuckDuckGo** | Fallback (no key required) | – |
| **Firecrawl** | Intelligent web scraping | api_key |
| **Playwright** | Headless browser (JS-heavy sites) | None |

**Search Strategy:**
1. Try Tavily + SerpAPI in parallel (if keys available)
2. Merge and deduplicate results
3. Fallback to DuckDuckGo if both fail
4. Never stop the scan due to search failure

### 🤖 LLM — Groq

| Model | Purpose | Settings |
|-------|---------|----------|
| `openai/gpt-oss-120b` | Supply extraction + demand signal detection | Temperature 0.3, JSON mode |

**Cost:**
- Supply scan: ~800–1,200 tokens per company
- Demand scan: ~500–700 tokens per company
- Insights: ~300 tokens per article

---

## 🚀 Deployment & Setup

### Local Development 💻

```bash
# Clone repo
git clone <repo-url>
cd Scout

# Setup backend
cd backend
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# Setup frontend
cd ../frontend
npm install

# Environment variables
cp backend/.env.example backend/.env
cp frontend/.env.example frontend/.env

# Add your keys:
# TAVILY_API_KEY=
# SERP_API_KEY=
# FIRECRAWL_API_KEY=
# GROQ_API_KEY=
# DATABASE_URL=postgresql://...
# NEXT_PUBLIC_API_URL=http://localhost:8000

# Start services
# Terminal 1:
cd backend && ./run_dev.sh

# Terminal 2:
cd frontend && npm run dev

# Access:
# Frontend: http://localhost:3000
# Backend: http://localhost:8000
# Docs: http://localhost:8000/docs
```

### Production Deployment 🌐

#### Backend (Railway)
```bash
git push origin main
# Railway auto-detects, builds Docker, deploys
# Status: railway.app
```

#### Frontend (Vercel)
```bash
git push origin main
# Vercel auto-builds, deploys to CDN
# Status: vercel.com/dashboard
```

---

## ⚙️ Configuration

### Supply Scan Rules — `config/criteria.yaml`

```yaml
markets:
  - name: "SaaS"
    industries: ["Software", "Cloud", "Analytics"]
    team_size_min: 5
    funding_stage: ["Seed", "Series A", "Series B"]
    markets_of_interest: ["B2B", "Enterprise"]
    exclude_revenue_threshold: 100000000  # >$100M = too mature

scoring:
  team_quality: 0.3
  market_fit: 0.4
  funding_stage: 0.3

tiers:
  tier1: 85-100
  tier2: 60-84
  tier3: 40-59
```

### Demand Scan Rules — `config/demand_criteria.yaml`

```yaml
martech_need_signals: 9       # List of signals to detect
buying_capacity_signals: 9     # List of signals to evaluate
actionability_triggers: 9      # List of triggers to watch

windows:
  martech_need_months: 12      # Detection window
  actionability_months: 18     # Trigger window

minimum_thresholds:
  martech_need: 2              # At least 2 signals
  buying_capacity: 2           # At least 2 true signals
  actionability: 1             # At least 1 trigger

trusted_sources:
  - exchange4media.com
  - campaignindia.in
  - linkedin.com
  - crunchbase.com

max_pages_per_company: 12      # Don't search forever
```

### Exclusions — `config/filters.yaml`

```yaml
blocked_companies:
  - "Example Corp"
  - "Fake Inc"

blocked_domains:
  - "example.com"
  - "fakedomain.io"

exclusion_keywords:
  - "job board"
  - "glossary"
  - "roundup"
```

### Environment Variables

```env
# Search APIs
TAVILY_API_KEY=tvly_...
SERP_API_KEY=...

# Web scraping
FIRECRAWL_API_KEY=fc_...

# LLM
GROQ_API_KEY=gsk_...

# Database
DATABASE_URL=postgresql://user:pass@db.supabase.co/postgres
SUPABASE_URL=https://...supabase.co
SUPABASE_KEY=eyJ...

# Frontend
NEXT_PUBLIC_API_URL=https://api.scout.app
NEXT_PUBLIC_VERCEL_URL=https://scout.app
```

---

## 📱 UI Pages

### 1️⃣ **Dashboard** 📊
- 📈 Overview: recent scans, total leads found, conversion rates
- 🔄 Quick actions: Run Supply Scan, Run Demand Scan, View History
- 📋 Latest results preview

### 2️⃣ **Supply Scan** 🚀
- 🎯 Set criteria (industry, team size, funding stage)
- ▶️ Run scan with real-time progress
- 🏆 Results: Tier 1, 2, 3 companies
- 💾 Export as CSV/JSON
- 📊 Detailed company cards (funding, team, location, score)

### 3️⃣ **Demand Scan** 👥
- ➕ Add companies (name + optional domain)
- ▶️ Run scan with streaming progress
- ✅ View qualified leads (all 3 filters passed)
- 📋 Partial matches (incomplete, not ready yet)
- 🔍 Signal details (evidence quotes + sources + dates)
- 📊 Historical scans browser

### 4️⃣ **Insights** 📰
- 🔄 Refresh from configured sources
- 📰 Articles ranked by relevance
- 🏷️ Categories (news, funding, hiring, expansion)
- 📊 Trending topics

### 5️⃣ **Settings** ⚙️
- 📋 Supply criteria (YAML editor)
- 📋 Demand criteria (YAML editor)
- 🚫 Blocklists (companies, domains)
- 🔑 API key status
- 📊 Usage stats (searches, LLM calls)

---

## 🔒 Security & Performance

### Security ✅
- 🔐 API authentication (FastAPI middleware)
- 🛡️ Input validation (Pydantic)
- 🔒 Secrets in environment (never in config)
- 🚫 Rate limiting on API endpoints
- ✅ CORS configured (frontend domain only)

### Performance ⚡
- 🚀 Parallel search (Tavily + SerpAPI simultaneously)
- 📦 Result caching (Supabase + Redis)
- 🔄 Streaming progress (WebSocket)
- 📊 Database indexing (company names, dates)
- ⏱️ Timeouts on external API calls

### Error Handling 🛡️
- ✅ Failed search → fallback to DuckDuckGo
- ✅ Failed webpage → skip and continue
- ✅ Failed LLM → retry with backoff
- ✅ Failed company → record error and next
- ✅ All errors logged to `data/errors.log`

---

## 💰 Cost Optimization

### API Costs 💵

| Service | Est. Cost | Per |
|---------|-----------|-----|
| Tavily | ~$100–200 | Month |
| SerpAPI | ~$50–100 | Month |
| Firecrawl | ~$20–50 | Month |
| Groq | ~$10–30 | Month |
| Supabase | ~$25–50 | Month |

**Cost Savers:**
- ✅ DuckDuckGo fallback (free, no key)
- ✅ Deduplication (don't re-scan same domain)
- ✅ Caching (don't re-fetch same website)
- ✅ LLM batching (combine multiple extractions)

### Scan Efficiency

| Metric | Typical |
|--------|---------|
| Supply scan (50 companies) | 3–5 minutes |
| Demand scan (25 companies) | 2–4 minutes |
| API calls per company | 3–5 (search + scrape + extract) |
| Cost per company | $0.15–0.35 |

---

## 📈 Design Principles

### 1️⃣ **Evidence-Based Ranking** 📊
- Every score is justifiable (team × market × funding)
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
- Criteria editable via UI
- Settings versionable and auditable

### 5️⃣ **Time-Based Decision Making** ⏱️
- MarTech Need: last 12 months (recent trends)
- Actionability: last 18 months (ready-to-buy window)
- Signal dating: capture and validate dates

---

## 🧪 Testing

```bash
# Backend tests
cd backend
pytest                          # All tests
pytest tests/test_search.py     # Search provider
pytest tests/test_extract.py    # LLM extraction
pytest tests/test_demand.py     # Demand logic
pytest --cov=pipeline          # Coverage

# Frontend tests
cd frontend
npm test                        # Jest tests
npm run build                   # Prod build check
```

---

## 📁 Project Structure

```
Scout/
├── 🎨 frontend/               (Next.js + Vercel)
│   ├── src/
│   │   ├── app/
│   │   │   ├── page.tsx        (Dashboard)
│   │   │   ├── supply/
│   │   │   ├── demand/
│   │   │   ├── insights/
│   │   │   └── settings/
│   │   ├── components/
│   │   │   ├── ScanProgress.tsx
│   │   │   ├── ResultsTable.tsx
│   │   │   └── Charts/
│   │   ├── hooks/
│   │   │   ├── useScan.ts
│   │   │   ├── useDemand.ts
│   │   │   └── useExport.ts
│   │   └── lib/
│   │       ├── api.ts          (API client)
│   │       └── utils.ts
│   ├── public/
│   └── package.json
│
├── 🔧 backend/                (FastAPI + Railway)
│   ├── api/
│   │   ├── main.py
│   │   ├── supply_main.py
│   │   └── demand_main.py
│   ├── pipeline/
│   │   ├── pipeline_runner.py
│   │   ├── demand/
│   │   │   └── runner.py
│   │   └── stages/
│   │       ├── search.py
│   │       ├── filter.py
│   │       ├── scrape.py
│   │       └── extract.py
│   ├── utils/
│   │   ├── search_provider.py
│   │   ├── web_scraper.py
│   │   ├── llm_client.py
│   │   └── dedup.py
│   ├── config/
│   │   ├── criteria.yaml
│   │   ├── demand_criteria.yaml
│   │   ├── filters.yaml
│   │   └── settings.yaml
│   ├── db/
│   │   ├── models.py
│   │   └── connection.py
│   ├── requirements.txt
│   ├── Dockerfile
│   ├── railway.yml
│   └── .env.example
│
├── 📊 data/
│   ├── results.csv / .json
│   ├── demand_results.json
│   ├── excluded.csv
│   ├── runs/               (timestamped snapshots)
│   ├── insights.json
│   └── errors.log
│
├── 📋 config/              (YAML files)
│   └── criteria.yaml, demand_criteria.yaml, filters.yaml
│
└── 📚 docs/
    ├── SETUP.md
    ├── API_REFERENCE.md
    └── ARCHITECTURE.md
```

---

## 🎯 API Endpoints

### Dashboard
```
GET  /api/dashboard            # Overview metrics
GET  /api/health               # Service status
```

### Supply Scan
```
POST /api/supply/scan          # Start new supply scan
GET  /api/supply/results       # Latest supply results
GET  /api/supply/history       # Past supply scans
GET  /api/supply/progress/{id} # Real-time progress
```

### Demand Scan
```
POST /api/demand/scan          # Start new demand scan
GET  /api/demand/leads         # Qualified leads
GET  /api/demand/history       # Past demand scans
GET  /api/demand/criteria      # Current criteria
GET  /api/demand/progress/{id} # Real-time progress
```

### Insights
```
GET  /api/insights             # Latest insights
POST /api/insights/refresh     # Fetch new articles
```

### Settings
```
GET  /api/settings             # All settings
PUT  /api/settings/criteria    # Update criteria
PUT  /api/settings/filters     # Update filters
```

---

## 🚀 Future Roadmap

### Phase 2 (Q4 2024)
- 🤖 **AI-powered outreach templates** — generate emails per company
- 📞 **CRM integration** — sync leads to Salesforce/HubSpot
- 📊 **Pipeline analytics** — track conversion rates
- 🔔 **Alert system** — notify when new high-quality leads appear

### Phase 3 (2025)
- 🌍 **International expansion** — support multiple countries
- 📱 **Mobile app** — iOS/Android native apps
- 🎬 **Video intelligence** — analyze founder/CEO videos
- 🤝 **Collaboration features** — team notes, deal tracking

---

## 🤝 Contributing

### Before You Start
1. Review [ARCHITECTURE.md](docs/ARCHITECTURE.md)
2. Check criteria.yaml/demand_criteria.yaml (don't hardcode)
3. Test with real companies before merging

### Code Standards
- ✅ Type hints (Python + TypeScript)
- ✅ Docstrings on functions
- ✅ Config-driven (no hardcodes)
- ✅ Test coverage >80%
- ✅ Fallbacks for external APIs

### PR Checklist
- [ ] Tests pass locally
- [ ] Config changes documented
- [ ] External API calls have timeouts
- [ ] Errors logged to errors.log
- [ ] Frontend shows user-friendly messages

---

## 📖 Documentation

| Document | Purpose |
|----------|---------|
| **README.md** | Overview, setup, quick start |
| **PROJECT_WORKFLOW_SIMPLE.md** | Plain-language guide to all features |
| **PROJECT_WORKFLOW.md** | Detailed technical workflow |
| **demand_agent.md** | Demand scan signal specifications |
| **ARCHITECTURE.md** | System design, data flow, invariants |
| **API_REFERENCE.md** | All endpoints, schemas, examples |

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
- LLM retries automatically 3 times
- Failed extractions logged to `data/errors.log`

---

## 📜 License

**Proprietary** — Enterprise lead generation platform.

---

## 📊 Metrics & Stats

| Metric | Typical |
|--------|---------|
| **Scans per week** | 5–10 |
| **Companies per scan** | 50–250 |
| **Qualified leads per month** | 15–45 |
| **Scan time (50 companies)** | 3–5 minutes |
| **False positive rate** | <5% (3-filter validation) |
| **Data freshness** | Real-time (within 24h) |

---

## 🎉 Built With ❤️

**Frontend:** Next.js + React + Vercel  
**Backend:** FastAPI + Python + Railway  
**Data:** Supabase + PostgreSQL  
**Search:** Tavily + SerpAPI + DuckDuckGo  
**Scraping:** Firecrawl + Playwright  
**LLM:** Groq (gpt-oss-120b)

---

**Last Updated:** September 2024  
**Status:** Production Ready ✅  
**Version:** 2.0 (Full-Stack Intelligence)

---

![Image #4: Scout Results Dashboard]
![Image #5: Qualified Leads View]
![Image #6: Signal Evidence]
