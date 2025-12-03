# H-001 | The Automated Insight Engine
**Tagline:** An event-driven data pipeline that converts raw campaign CSVs into executive-ready PowerPoint decks with AI-generated narratives in under a minute.

1. The Problem (Real World Scenario)
- **Context:** Marketing ops teams burn hours each week manually downloading CSVs, plotting charts, and assembling “Weekly Performance” decks.
- **Pain Point:** Slow, tedious, error-prone. When a campaign underperforms, the client learns days late because reporting lags.
- **My Solution:** Drop a raw file into the project, and minutes later you have a polished PPTX with charts and an AI narrative ready to send.

1. Expected End Result
- **Input:** A raw marketing campaign CSV (uplift, channel, objective, dates, segment).
- **Action:** Run the notebook or script; wait under a minute.
- **Output:** A PowerPoint deck containing:
  - Uplift charts by channel and objective.
  - Tables of top-performing channels and segments.
  - An AI-written executive summary tailored to the data.

1. Technical Approach
- **Clean & Validate:** Normalize column names, coerce dates and numerics, drop incomplete rows.
- **Feature Engineering:** Compute campaign duration; derive start month for temporal rollups.
- **Aggregation:** Build summary tables (overall, channel, objective, segment, start month).
- **Visualization:** Matplotlib renders uplift-by-channel and uplift-by-objective charts.
- **Narrative Generation:** OpenAI (`gpt-5-mini` by default) turns stats into an executive narrative with guardrails (strict context prompt).
- **Reporting:** `python-pptx` assembles title, overview, tables, charts, and the AI insight slide into a single deck.

1. Tech Stack
- **Language:** Python
- **Data:** Pandas (ETL + aggregation)
- **Visualization:** Matplotlib
  - **AI Model:** OpenAI `gpt-4o-mini` (configurable)
- **Reporting:** python-pptx
- **Data Source:** KaggleHub for campaign CSVs (dataset: https://www.kaggle.com/datasets/geethasagarbonthu/marketing-and-e-commerce-analytics-dataset)

1. Challenges & Learnings
- **AI Hallucinations:** Early drafts over-claimed. Fixed via a strict context prompt and grounding the narrative on computed stats only.
- **Data Quality:** Incoming CSVs varied in schema. Added normalization, type coercion, and drop rules for incomplete records to keep summaries trustworthy.

1. Visual Proof
- Uplift-by-channel bar chart (Matplotlib)
- Uplift-by-objective bar chart (Matplotlib)
- Final PowerPoint deck with AI-generated “Executive Insights” slide

1. How to Run
- **Prereqs:** Python; environment variable `OPENAI_API_KEY` set (e.g., in `.env`).
- **Install deps:** `pip install pandas matplotlib python-pptx kagglehub openai python-dotenv`
- **Execute:** Run `main.ipynb` top to bottom (downloads dataset via KaggleHub, processes data, generates charts, calls the LLM, builds PPTX).
- **Output:** `output/Marketing_Insight_Engine_Deck.pptx` plus chart PNGs in `output/`.
- **Config:** Adjust model via `OPENAI_MODEL` in the notebook; change dataset by pointing KaggleHub to a different source or swapping in your CSV path.
