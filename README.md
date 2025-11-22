# Consumer Perception on Electric Vehicles Using Sentiment Analysis (Karnataka)

<img width="946" height="532" alt="image" src="https://github.com/user-attachments/assets/0e07e90c-31b3-49c4-9278-b7734fc54779" />



End-to-end analytics project that combines **EV 2-wheeler sales data from Karnataka** with **consumer sentiment** from reviews/social channels to understand what really drives adoption in the state.  

The repository contains the full workflow: **project planning, data engineering, NLP sentiment modelling, correlation analysis, and an interactive Power BI dashboard**.

---

## 🔍 1. Project Overview

EV 2-wheelers are growing fast in **Karnataka**, but adoption depends heavily on how customers feel about **range**, **charging**, **price**, **service quality**, and **build**.

This project:

- Collects 12 months of EV consumer voice (reviews/forums/social posts) and sales data **specific to Karnataka**.
- Builds a sentiment model to classify feedback as **positive** or **negative**.
- Links sentiment trends to **brand/model sales in Karnataka**.
- Delivers a **self-serve dashboard** for product, marketing, and leadership teams.

**Key outcomes (high level)**

- ~**90.5%** test accuracy and **85.8%** validation accuracy for sentiment classification (Naive Bayes).
- Dashboard covering **19 EV models** and **561 reviews** from Karnataka, with **3.34/5** average rating and **3.55/5** comfort score.
- Clear evidence that **ratings alone are not a good predictor of sales**, and that a few **core drivers** explain most sentiment.

---

## 🎯 2. Business Objective

The business objective is to **turn unstructured consumer feedback from Karnataka into actions**:

1. Identify the **top positive and negative drivers** influencing EV perception in Karnataka (e.g., range anxiety, charging ease, TCO, service experience, build quality).
2. Quantify how sentiment shifts relate to **sales movement over time** by brand/model within the state.
3. Ship a **dashboard + executive brief** that converts insights into **positioning, product and after-sales actions** for the Karnataka market.
4. Establish a simple **quarterly refresh process** (data → model → dashboard).

---

## 🧭 3. Project Management Highlights

This repo also showcases **project management skills** (for PM / PMO / Analytics PM roles).

### 3.1 Scope

**In scope**

- Collect 12-month data from:
  - EV 2-wheeler **reviews/forums/social posts** (English/Hinglish) relevant to Karnataka users.
  - **Monthly sales in Karnataka** by brand/model.
  - **Technical specs/features** (range, battery capacity, price segment, etc.).
- Processes:
  - ETL/ELT, cleaning, language detection, tokenization, normalization.
  - Sentiment modelling and evaluation.
  - Correlation and trend analytics.
  - Dashboard and executive deck.
- Governance:
  - Data dictionary, quality checks, experiment tracking.
  - UAT and sign-off.

**Out of scope**

- Pan-India analysis or cross-state comparison.
- Primary research (surveys/FGDs).
- Real-time streaming.
- CRM integration or campaign execution.

### 3.2 Stakeholders

Typical stakeholder set:

- **Sponsor:** wants business impact, timelines, and risk visibility.
- **Project Manager (you):** owns scope, schedule, budget, and RAID.
- **Data Engineering Lead:** responsible for pipelines, data quality, and infra.
- **NLP Lead / Data Scientist:** owns model performance and retraining.
- **Insights Analyst:** turns outputs into business stories and recommendations.
- **Dashboard Developer:** ensures usability and slicing/dicing.
- **Marketing / Product / CX:** consume insights and execute actions.

### 3.3 WBS, PERT & Critical Path

The work is broken down into:

1. **Initiation & Planning** – charter, scope, RACI, risk register, schedule.
2. **Data Engineering** – source discovery/access, schemas, ingestion, cleaning, QA.
3. **Modelling & Analytics** – text prep, labelling strategy, model training & evaluation, correlation & trend analysis.
4. **Visualization & Delivery** – metrics definition, dashboard build, UAT, handover, runbook.

**PERT highlights**

- Total effort: **~40.5 person-days**.
- Expected duration (critical path): **~28.9 days**.
- Critical path: `A → B → D → E → G → I`.

This structure makes the project easy to present from a **project manager** perspective.

---

## 🧱 4. Data & Sources

Typical data used (anonymised / synthetic where needed):

- **Reviews & Social Text**
  - EV 2-wheeler reviews (English/Hinglish) from customers in Karnataka.
  - Forum discussions and selected social posts related to EV usage in Karnataka.
  - Fields: `text`, `date`, `brand`, `model`, `city/district`, `rating`, `platform`.

- **Sales Data (Karnataka)**
  - Monthly sales per brand/model within Karnataka.
  - Fields: `month`, `brand`, `model`, `units_sold`, `city/district`.

- **Specifications / Features**
  - Range, battery capacity, price band, category, etc.

---

## 🛠️ 5. Tech Stack

- **Language:** Python
- **Libraries (typical)**: `pandas`, `numpy`, `scikit-learn`, `matplotlib/plotly`, `nltk`/`spaCy`
- **Modelling:** Naive Bayes (baseline) + room to plug SVM/LogReg/Transformers
- **Storage/Files:** CSV/Parquet
- **Visualization:** Power BI (dashboard), plus Python plots
- **Project Management Artifacts:** PDFs for slides/report (scope, WBS, PERT, risks, roadmap)

---

## 🧪 6. Methodology

### 6.1 Data Engineering

1. **Ingestion**
   - Load raw CSV/Excel files for reviews and sales.
   - Map brand/model names consistently.
   - Merge disparate sources into a unified table filtered for Karnataka.

2. **Cleaning**
   - Remove duplicates and junk rows.
   - Handle missing values.
   - Filter to target language (English/Hinglish).

3. **Standardization**
   - Normalize brand/model names.
   - Align dates to a monthly grain.
   - Join with specs and sales.

Outputs are written to `data/processed/`.

---

### 6.2 NLP & Sentiment Modelling

1. **Text Preprocessing**
   - Lowercasing and tokenization.
   - Stop-word removal.
   - Lemmatization.
   - Handling emojis, hashtags, and negations (e.g., “not good”).

2. **Feature Engineering**
   - TF-IDF vectors (1–2-grams).
   - Optional features from domain lexicons for range/charging/price/service.

3. **Model Training**
   - Baseline: **Multinomial Naive Bayes**.
   - Split into train / validation / test.
   - Train and tune simple hyperparameters.

4. **Evaluation**
   - Accuracy, precision, recall, and F1 per class.
   - Confusion matrix, especially for the **negative class** (to monitor complaint-miss risk).
   - Observed:
     - Test accuracy ~**90.5%**
     - Validation accuracy ~**85.8%**
     - Negative class has higher miss rate → keep manual review for spikes.

---

### 6.3 Sentiment ↔ Sales / Features Correlation (Karnataka)

1. Aggregate data to:
   - **Brand–month (Karnataka)**
   - **Model–month (Karnataka)**
   - **City/district–month**, if available.

2. Compute:
   - Average sentiment score.
   - Share of negative posts.
   - Review volume per period.
   - Monthly sales and key specs.

3. Run:
   - Pearson/Spearman correlations.
   - Lagged correlations (sentiment leading or lagging sales by 1–2 months).
   - Partial correlations controlling for price/promotions/seasonality (optional).

4. Interpret:
   - If correlation is weak, treat ratings/sentiment as **supporting, not leading** indicator.
   - Look for stable patterns across multiple months before using as a forecast input.

---

### 6.4 Dashboard

The Power BI dashboard (or equivalent BI tool) allows users to:

- Filter by **brand**, **model**, **city/district**, **sentiment**, and **time** (within Karnataka).
- View:
  - Market share by brand/model in Karnataka.
  - Trends in units sold over time.
  - Average ratings, reliability, performance, and comfort.
  - Sentiment distributions and top positive/negative themes.
<img width="1179" height="667" alt="image" src="https://github.com/user-attachments/assets/06ece8d3-5edd-4b0e-9938-7bd2e5be725a" />

This dashboard is the main **decision interface** for non-technical stakeholders.

---

## 📊 7. Key Results & Insights (Karnataka)

Some example insights from this project:

- **Ratings ≠ Sales**  
  Scatter plots and correlation heatmaps show **little to no linear relationship** between average ratings and sales volumes at the Karnataka level. Ratings help explain **why** customers feel a certain way, but not necessarily **how many** will buy.

- **Core Drivers of Sentiment**
  - **Price/Value**
  - **Charging & Range**
  - **Service Experience**
  - **Build Quality**
  - **Features / Comfort**

- **Brand-level Storylines (Karnataka)**
  - Some brands lead in **market share** but not always in **reliability or ratings**.
  - Certain mid-pack models (e.g., with good reliability scores) are strong candidates for **growth campaigns**.
  - A few models show **consistently low ratings**, signalling need for **product or service fixes**.

- **Analytics to Action**
  - Marketing messages can focus on **range confidence**, **charging ease**, and **TCO**.
  - Product and operations can prioritize **charging infra, service TAT, and build-quality fixes**.
  - CX teams can set up **alerts for negative sentiment spikes** and respond within 24–48 hours.

---

## 📁 8. Repository Structure (Suggested)

```bash
.
├── data/
│   ├── raw/                 # Raw review / sales / specs data (not tracked in git)
│   └── processed/           # Cleaned and merged datasets
├── notebooks/
│   └── Evbike__sentimentAnalysis.ipynb   # Main analysis & modelling notebook
├── src/
│   ├── data_pipeline/       # ETL / cleaning scripts
│   ├── models/              # Training / evaluation scripts
│   └── viz/                 # Plots / dashboard export helpers
├── reports/
│   ├── EV_Presentation_Grp6.pdf
│   └── Group6-Report-Consumers-Perception-on-EV-Sentiment-Analysis.pdf
└── README.md

```
## 🚀 9. Getting Started

### 9.1 Prerequisites

- Python 3.9+
- Recommended: virtual environment (`venv` or `conda`)
- Power BI Desktop (or any BI tool you prefer) if you want to open/modify the dashboard.

### 9.2 Installation

Clone the repository and set up your environment:

    git clone https://github.com/<your-username>/ev-consumer-sentiment-sales-analytics-karnataka.git
    cd ev-consumer-sentiment-sales-analytics-karnataka

Create and activate a virtual environment:

- On macOS / Linux:

    python -m venv .venv
    source .venv/bin/activate

- On Windows:

    python -m venv .venv
    .venv\Scripts\activate

Install dependencies:

    pip install -r requirements.txt

You can generate `requirements.txt` from your environment using:

    pip freeze > requirements.txt

### 9.3 Running the Notebook

Launch Jupyter Notebook:

    jupyter notebook notebooks/Evbike__sentimentAnalysis.ipynb

Follow the notebook cells in order:

1. Load data.
2. Clean and preprocess text.
3. Train and evaluate the sentiment model.
4. Export outputs for the dashboard (aggregated metrics by brand/model/city).

---

## 🔄 10. Future Improvements

- Add **aspect-based sentiment analysis** (separate scores for range, charging, price, service, build).
- Plug in a **Transformer-based model** (e.g., BERT) and compare performance with Naive Bayes.
- Extend data sources to more forums and regional languages within Karnataka.
- Automate **quarterly retraining and dashboard refresh**.
- Integrate with CRM or campaign tools to trigger **personalized outreach** based on sentiment signals.
- Deploy the model as an API/microservice and connect it to real-time feedback channels.

---

## 🙌 11. Acknowledgements

- **Faculty and mentors** for guidance on both analytics and project management.
- **Team members** for contributions to data engineering, NLP, visualization, and storytelling.
- **Public EV datasets and review platforms** that made this analysis possible.
- The broader **open-source community** for libraries and tools that power this project.
