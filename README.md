# ConsumerShield — AI-Powered Consumer Complaint & Emerging Issue Intelligence

## Project Overview
ConsumerShield analyzes publicly available consumer financial complaint data to understand
what problems consumers are facing, how those problems are trending over time, which
underlying themes drive them, and where emerging issues may need attention — using Data
Analytics, NLP (semantic analysis), and Machine Learning.

## Problem Statement
Financial institutions and regulators receive large volumes of consumer complaints. Manually
reading and categorizing them to spot recurring problems and emerging risks is impractical.
ConsumerShield uses NLP and analytics to automatically surface these patterns.

## Objectives
- Summarize complaint data into clear KPIs
- Detect recurring complaint themes from free-text narratives (semantic/NLP analysis)
- Build a similar-complaint search tool
- Track complaint trends over time
- Flag potential emerging issues, with safeguards against false alarms
- Analyze complaint patterns by company (without unfair "worst company" labeling)

## Dataset
**Source:** CFPB (Consumer Financial Protection Bureau) Consumer Complaint Database — archived
narratives, publicly available at
https://www.consumerfinance.gov/data-research/consumer-complaints/

**File used:** `CCDB_Export_5_September_2023_through_March_2024.zip` (Sep 2023 – Mar 2024)

**Note:** CFPB stopped publishing new complaint narratives after 14 August 2026. This project
uses the previously published historical archive, which remains publicly downloadable.

## Technologies Used
- Python
- Pandas, NumPy
- scikit-learn (TF-IDF, KMeans clustering, Logistic Regression, cosine similarity)
- Matplotlib
- SQLite (SQL analysis)
- python-docx (report generation)

## Project Workflow
1. Download and inspect the CFPB complaint export
2. Filter to complaints with a written narrative; sample 40,000 for NLP/ML
3. Clean text (remove CFPB's "XXXX" redaction noise) and derive a monthly date field
4. Compute overview KPIs
5. Trend analysis (monthly complaint volume)
6. Theme detection via TF-IDF + KMeans clustering (8 themes)
7. Product classifier (Logistic Regression on TF-IDF features)
8. Similar-complaint search (TF-IDF cosine similarity)
9. Emerging issue detection with a minimum-volume filter and "review required" labeling
10. Company-level complaint summary
11. SQL aggregation queries (SQLite)

## How to Run
1. Open `YourName_ConsumerShield.ipynb` in Jupyter or Google Colab
2. Run all cells top to bottom (the notebook downloads the dataset automatically)
3. Install dependencies first if running locally: `pip install -r requirements.txt`

## Key Findings
- Of 945,532 total complaints in this period, 318,804 (33.7%) included a written narrative
- Timely response rate across companies: 99.5%
- Top product: Credit reporting or other personal consumer reports
- Top issue: Incorrect information on your report
- The three major credit bureaus (TransUnion, Equifax, Experian) account for the largest
  share of complaints, consistent with credit reporting being the dominant issue category
- A Logistic Regression classifier predicts complaint product from narrative text with
  88.1% accuracy
- 8 NLP-derived themes: legal/FCRA dispute language, late payment reporting, debt/loan
  disputes, identity theft & fraud, credit reporting legal citations, complaint process
  frustration, fraudulent accounts/inquiries, and bureau validation requests
- Potential emerging issues (flagged for review, not confirmed): "Written notification about
  debt" (+90%, n=524) and "Attempts to collect debt not owed" (+41%, n=606)

## Limitations
- NLP/ML analysis is based on a 40,000-complaint sample, not the full dataset
- CFPB states its complaint database is not a statistical sample of all consumer experiences
- Emerging-issue flags are statistical signals for review, not confirmed problems
- Company complaint counts are not adjusted for company size/market share

## Future Scope
- Sentence embeddings for improved semantic similarity
- Interactive Power BI dashboard (CSV exports `powerbi_monthly_trend.csv` and
  `powerbi_company_summary.csv` are already generated for this purpose)
- Extension to Indian consumer/banking complaint data
- GenAI/RAG-based natural-language querying over complaints

## Conclusion
ConsumerShield demonstrates an end-to-end consumer complaint analytics pipeline — from raw
text to KPIs, trends, NLP-driven themes, a classifier, semantic search, and cautious
emerging-issue detection — built for the IBM SkillsBuild Data Analytics with AI Academic
Internship (BharatCares, in association with AICTE).
