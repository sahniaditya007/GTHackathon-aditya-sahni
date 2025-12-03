H-001 | The Automated Insight Engine
Tagline: An event-driven data pipeline that converts raw campaign CSVs into executive-ready PowerPoint decks with AI-generated narratives in under a minute.

1. The Problem (Real World Scenario)
- Context: Marketing teams spend hours every week downloading CSVs, plotting charts, and assembling “Weekly Performance” slides for stakeholders.
- Pain Point: The workflow is slow and repetitive, and when a campaign underperforms, clients often learn about it days late due to reporting delays.
- My Solution: Drop a raw file into the project, run the pipeline, and within minutes you receive a polished PPTX containing charts and a clear AI-generated explanation of performance.

2. Expected End Result
- Input: A raw marketing campaign CSV (fields like uplift, channel, objective, dates, and segment).
- Action: Run the notebook or script; wait under a minute.
- Output: A complete PowerPoint deck with:
  - Uplift charts by channel and by objective
  - Tables highlighting top-performing channels and segments
  - An AI-generated executive summary grounded in the dataset

3. Technical Approach
- Clean & Validate: Standardizes column names, parses dates, converts numerics, and removes incomplete records.
- Feature Engineering: Computes campaign duration and extracts start month for trend analysis.
- Aggregation: Builds summary tables across overall performance, channel, objective, segment, and monthly rollups.
- Visualization: Uses Matplotlib to generate uplift-by-channel and uplift-by-objective bar charts.
- Narrative Generation: Google Gemini (gemini-2.5-flash by default) transforms aggregated stats into an executive-level narrative using a strict context prompt for grounding.
- Reporting: python-pptx assembles all elements—title, overview, tables, charts, and AI insights—into a polished final deck.

4. Tech Stack
- Language: Python
- Data Processing: Pandas (ETL + aggregation)
- Visualization: Matplotlib
- AI Model: Google Gemini (gemini-2.5-flash, configurable)
- Reporting: python-pptx
- Data Source: KaggleHub (dataset: https://www.kaggle.com/datasets/geethasagarbonthu/marketing-and-e-commerce-analytics-dataset)

5. Challenges & Learnings
- AI Stability: Early narrative drafts were too general. Solved by grounding the LLM strictly on computed summary statistics.
- Data Quality Variations: The dataset schema didn’t fully match typical AdTech metrics. Added normalization and type coercion to make the pipeline robust across different incoming CSVs.

6. Visual Proof
- Uplift-by-channel bar chart (Matplotlib)
- Uplift-by-objective bar chart (Matplotlib)
- Final PowerPoint deck including an AI-generated “Executive Insights” slide

7. How to Run
- Prereqs: Python; environment variable GEMINI_API_KEY set (ideally in a `.env` file).
- Install deps:
  pip install pandas matplotlib python-pptx kagglehub google-genai python-dotenv
- Execute:
  - Open and run main.ipynb from top to bottom.
  - The notebook downloads the dataset via KaggleHub, cleans and processes the data, generates charts, calls Gemini for the narrative, and builds the final PPTX.
- Output:
  - output/Marketing_Insight_Engine_Deck.pptx
  - Chart PNGs saved in output/
- Config:
  - Change Gemini model by editing GEMINI_MODEL in the notebook.
  - Use a different dataset by updating the KaggleHub path or loading your own CSV.
