# Mini Project 3 — Agentic AI in FinTech

## Project Overview

Comparing Baseline, Single-Agent, and Multi-Agent architectures for financial Q&A using live stock data, fundamentals, and news sentiment.

## Structure

```
├── app.py                    # Streamlit chat interface
├── mp3_assignment_yvette.ipynb  # Notebook with analysis & reflection Q0–Q5
├── config.py                 # API keys, model settings
├── tools.py                  # 7 tool functions (yfinance + Alpha Vantage + SQLite)
├── schemas.py                # OpenAI tool schemas
├── benchmark_questions.py    # 15 fixed evaluation questions
├── run_evaluation.py         # Run full evaluation → Excel
├── agents/
│   ├── baseline_agent.py
│   ├── single_agent.py
│   ├── multi_agent_runner.py
│   └── multi-agent/
│       ├── orchestrator.py
│       ├── market_specialist.py
│       ├── fundamentals_specialist.py
│       ├── sentiment_specialist.py
│       ├── critic.py
│       └── synthesizer.py
├── evaluation/
│   ├── evaluator.py
│   └── evaluation_runner.py
├── results/
│   ├── results_gpt4o_mini.xlsx
│   └── results_gpt4o.xlsx
├── screenshots/              # Streamlit deployment screenshots
├── chechin_report/           # Mid-project check-in materials
├── stocks.db                 # Local SQLite DB (S&P 500 companies)
└── sp500_companies.csv       # Source data
```

## Setup

```bash
pip install -r requirements.txt
```

Create a `.env` file:
```
OPENAI_API_KEY=sk-...
ALPHAVANTAGE_API_KEY=...
```

## Run Streamlit App

```bash
python -m streamlit run app.py
```

## Run Evaluation

```bash
# gpt-4o-mini
python run_evaluation.py

# gpt-4o
python run_evaluation.py large
```

## Multi-Agent Architecture

**Orchestrator + Specialists + Critic**

1. **Orchestrator** — reads question, plans which specialists are needed
2. **Market Specialist** — price performance, market status, sector lists
3. **Fundamentals Specialist** — P/E, EPS, market cap, 52-week range
4. **Sentiment Specialist** — news headlines and sentiment scores
5. **Critic** — verifies each specialist answer against raw tool data
6. **Synthesizer** — combines verified results into final answer

## Results Summary (gpt-4o-mini)

| Architecture | Easy | Medium | Hard | Overall |
|---|---|---|---|---|
| Baseline | 26.7% | 6.7% | 0% | 11.1% |
| Single Agent | 40.0% | 33.3% | 20.0% | 31.1% |
| Multi-Agent | 40.0% | 40.0% | 46.7% | **42.2%** |
