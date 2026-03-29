# ET AI-Native News Experience

> **ET AI Hackathon 2026 — Problem Statement 8**

An AI-powered news platform that fundamentally reimagines how business news is consumed. Not just a filtered feed — a personalized, interactive, multilingual intelligence layer built on top of news data.

## Features

### 1. My Newsroom — Personalized Feed
AI curates your news based on your role (investor/founder/student) and interests. Every user gets a different front page with personalized hooks explaining why each story matters to *them*.

### 2. Intelligence Briefing
Instead of reading 10 articles about the same topic, get ONE synthesized deep briefing with executive summary, key developments, market implications, and interactive follow-up Q&A.

### 3. Story Arc Tracker
Track any ongoing business story with an AI-generated timeline, key player mapping, sentiment shifts, contrarian views, and predictions.

### 4. Vernacular Business News
Context-aware translation into 8 Indian languages — Hindi, Tamil, Telugu, Bengali, Marathi, Gujarati, Kannada, Malayalam. Not literal translation — culturally adapted with local context.

### 5. Smart Summarizer
Same article, 4 different summaries: Brief, Explainer (student-friendly), Investor (market focus), Founder (opportunity focus).

## Tech Stack

| Component | Technology | Cost |
|-----------|-----------|------|
| LLM (Primary) | Groq — Llama 3.3 70B | Free |
| LLM (Fallback) | Google Gemini 2.0 Flash | Free |
| News Data | SerpApi Google News | Free/paid |
| Backend | FastAPI | Open source |
| Frontend | Streamlit | Open source |
| Language | Python 3.10+ | - |

## Setup

### 1. Clone & Install

```bash
git clone <repo-url>
cd hack
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### 2. Get Free API Keys

- **Groq**: Sign up at [console.groq.com](https://console.groq.com) → Create API key
- **SerpApi**: Sign up at [serpapi.com](https://serpapi.com) → Get API key for Google News
- **Gemini** (optional fallback): [aistudio.google.com](https://aistudio.google.com) → Get API key

### 3. Configure Environment

```bash
cp .env.example .env
# Edit .env with your API keys
```

### 4. Run

**Streamlit UI (recommended):**
```bash
streamlit run frontend/app.py
```

**FastAPI backend (API only):**
```bash
uvicorn app.main:app --reload
```

## Architecture

```
┌─────────────────────────────────────────────────────┐
│                  Streamlit Frontend                  │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌────────┐ │
│  │My News-  │ │Briefing  │ │Story Arc │ │Vernacu-│ │
│  │room      │ │Navigator │ │Tracker   │ │lar     │ │
│  └────┬─────┘ └────┬─────┘ └────┬─────┘ └───┬────┘ │
└───────┼─────────────┼───────────┼────────────┼──────┘
        │             │           │            │
┌───────▼─────────────▼───────────▼────────────▼──────┐
│                   Agent Layer                        │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌────────┐ │
│  │Personal- │ │Briefing  │ │Story     │ │Trans-  │ │
│  │izer Agent│ │Agent     │ │Tracker   │ │lator   │ │
│  └────┬─────┘ └────┬─────┘ └────┬─────┘ └───┬────┘ │
└───────┼─────────────┼───────────┼────────────┼──────┘
        │             │           │            │
┌───────▼─────────────▼───────────▼────────────▼──────┐
│                  Service Layer                       │
│        ┌──────────────┐    ┌──────────────┐         │
│        │  News Fetcher │    │  LLM Service │         │
│        │  (SerpApi)    │    │  (Groq/Gemini│         │
│        └──────────────┘    └──────────────┘         │
└─────────────────────────────────────────────────────┘
```

## Agents

| Agent | Purpose | LLM Used |
|-------|---------|----------|
| Personalizer | Curates feed based on user profile | Groq (Llama 3.3) |
| Briefing | Synthesizes multi-source briefings | Groq (Llama 3.3) |
| Story Tracker | Builds narrative arcs from articles | Groq (Llama 3.3) |
| Translator | Culturally-adapted vernacular translation | Groq (Llama 3.3) |
| Summarizer | Multi-style article summaries | Groq (Llama 3.3) |

All agents fall back to Gemini 2.0 Flash if Groq is unavailable.

## Team

Built for ET AI Hackathon 2026 — Problem Statement 8: AI-Native News Experience
