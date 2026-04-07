<div align="center">

```
 █████╗ ███╗   ██╗███╗   ███╗ ██████╗ ██╗
██╔══██╗████╗  ██║████╗ ████║██╔═══██╗██║
███████║██╔██╗ ██║██╔████╔██║██║   ██║██║
██╔══██║██║╚██╗██║██║╚██╔╝██║██║   ██║██║
██║  ██║██║ ╚████║██║ ╚═╝ ██║╚██████╔╝███████╗
╚═╝  ╚═╝╚═╝  ╚═══╝╚═╝     ╚═╝ ╚═════╝ ╚══════╝
```

### Data Analyst & ML Engineer · Turning Raw Data Into Decisions

[![Football Analytics](https://img.shields.io/badge/⚽_Football_Analytics-Live_App-crimson?style=for-the-badge)](https://man-united-post-season-performance-analysis.streamlit.app/)
[![GitHub](https://img.shields.io/badge/GitHub-anmolzz--10-181717?style=for-the-badge&logo=github)](https://github.com/anmolzz-10)

</div>

---

## 👋 About Me

I'm a data analyst and machine learning engineer who builds things end-to-end — from raw data and SQL pipelines to regression models, Power BI dashboards, and deployed web applications. My work sits at the intersection of rigorous analysis and clean engineering: every project here goes beyond notebooks to deliver something usable, explainable, and production-aware.

I work across the full analytics stack — **SQL → Python → ML → BI → Deployment** — and care deeply about making technical findings accessible to non-technical stakeholders. Every project in this profile includes methodology documentation that speaks to both audiences.

---

## 🗂️ Project Portfolio

---

### ⚽ [Football Analytics — Manchester United 2024–25 Post-Season Investigation](https://github.com/anmolzz-10/Football-analytics)

> *Why did Manchester United finish 15th — 32 points off a Champions League place? A full data-science investigation.*

**🔗 [Live App →](https://man-united-post-season-performance-analysis.streamlit.app/)**

**The Question:** Was United's historic collapse due to bad luck, poor tactics, individual failures, or something structural?

**The Approach:**

This project answers that question the way modern football clubs do — with data. Using Expected Goals (xG) and Expected Goals Against (xGA) data from Understat across **three consecutive Premier League seasons** (2022–25, 60 total club-season observations), the analysis:

1. **Defines the Top 4 standard** — what attacking and defensive performance actually qualifies a team for Champions League
2. **Quantifies the gap** — United were 0.562 xG/match below the benchmark in attack and 0.352 xGA/match above it defensively
3. **Models the cost in points** — a multivariate linear regression (R² ~0.85) translates per-match gaps into concrete point losses
4. **Separates structural vs efficiency failures** — distinguishing "they didn't create enough chances" from "they wasted the chances they created"
5. **Diagnoses individual contributors** — player-level finishing efficiency analysis (goals minus xG)
6. **Simulates the fix** — interactive sliders let users project what a specific attacking or defensive improvement would yield in points

**Key Findings:**
- **70% of the 32.5-point deficit is structural** — explained directly by United's xG and xGA per-match levels, not variance
- Attacking shortfall cost ~**−14.9 points**; defensive exposure cost ~**−8.0 points**
- United underconverted their chances by **12.9 goals** across the season (conversion problem on top of a volume problem)
- **65% of all goal contributions** came from just 4 players — dangerous concentration
- Højlund (the designated striker) converted 4 goals from 5.87 xG — a finishing gap equivalent to ~5 lost points annually

**What is xG? (For non-technical readers):** Expected Goals is the probability that any given shot results in a goal, calculated from historical shot data. A tap-in from 6 yards has an xG of ~0.85. A long-range effort might have 0.03. Over 38 matches, xG is a far more reliable measure of team quality than actual goals scored — it removes luck.

**Stack:** `Python` · `Pandas` · `Scikit-learn` · `Plotly` · `Streamlit`

```
Data Flow:  Understat CSV (3 seasons) → Cleaning & Feature Engineering
         → Top 4 Benchmarking → Gap Analysis → Linear Regression
         → Finishing Efficiency → Player Diagnosis → Interactive Simulation
         → Narrative Dashboard (Streamlit)
```

---

### 🗄️ [SQL Finance & Market Analytics — AtliQ Hardware](https://github.com/anmolzz-10/sql-finance-detailed-analytics)

> *Advanced SQL analytics on a real-world hardware company database — from raw exploration to production-grade database objects.*

**The Problem:** AtliQ Hardware is a global electronics manufacturer selling across multiple markets and channels. Finance and supply chain teams need reliable, reusable systems to answer revenue, discount, and forecast questions — not just one-off queries.

**The Architecture:**

This project doesn't just write queries. It builds an **analytics infrastructure** across four layers:

| Layer | Object Type | What It Does |
|-------|------------|--------------|
| Logic | **User-Defined Function** `get_fiscal_year()` | Converts calendar dates to AtliQ's September-offset fiscal year — used by every date-based query |
| Reusability | **Stored Procedures** | Parameterised routines callable by any team or BI tool: monthly sales by customer, market Gold/Silver classification, top-N products per division |
| Pipeline | **Views** | Layered virtual tables: `gross_sales` → `net_invoice_sales`, mirroring Bronze/Silver/Gold data lakehouse architecture |
| Insight | **Window Functions** | `RANK()`, `DENSE_RANK()`, `SUM() OVER (PARTITION BY)` for rankings and contribution analysis |

**Business Questions Answered:**
- What did Croma India buy from AtliQ by product in FY2021?
- What is each customer's net invoice sales after their negotiated pre-invoice discount?
- Which customers forecast demand most accurately — and by how much do they deviate?
- How do products rank within their category on net sales?
- What % of regional revenue does each customer represent?

**Why the fiscal year UDF matters:** AtliQ's fiscal year starts in September. Without `get_fiscal_year()`, every JOIN between sales data and price tables would silently pull wrong-year prices. A November 2020 sale belongs to FY2021 — the UDF makes this correct everywhere, automatically.

**Why absolute error over net error in forecast accuracy:** Net error allows over- and under-forecasts to cancel out. A customer who over-forecasts by 500 units in January and under-forecasts by 500 in February shows zero net error — but has a real volatility problem. Absolute error captures both directions honestly.

**Stack:** `MySQL 8.0` · `Advanced SQL` · `UDFs` · `Stored Procedures` · `Views` · `CTEs` · `Window Functions`

```
Schema:  fact_sales_monthly + fact_gross_price → gross_sales (view)
                                              → net_invoice_sales (view)
         fact_act_est → Forecast Accuracy CTE → Customer Rankings
```

---

### 📊 [Sales Insights Dashboard — Power BI](https://github.com/anmolzz-10/sales-insights-power-bi)

> *A complete business intelligence solution connecting raw transactional data to executive-ready decisions across markets, customers, and products.*

**The Problem:** A multi-market sales organisation operating across Brick & Mortar and E-Commerce channels lacks a centralised system to answer: Where is revenue coming from? Are we profitable? Where are margins leaking?

**The Pipeline:**

```
MySQL Database → SQL Validation → Power BI Star Schema → DAX Measures → Interactive Dashboard
```

**Four Layers of the Solution:**

**1. SQL Trust Layer** — Before building any dashboard, all data is validated and explored in MySQL. Annual and monthly revenue queries establish baseline figures that the Power BI model must reproduce exactly. This is a common failure point in BI projects: dashboards that look great but show wrong numbers.

**2. Data Model (Star Schema)** — The transactional database is restructured into a star schema inside Power BI: `Transactions` fact table surrounded by `Customers`, `Products`, `Markets`, and `Date` dimension tables. This is the industry standard for BI systems and enables fast filtering and clean aggregation.

**3. DAX Intelligence Layer** — Business logic encoded as measures:
  - `Revenue` — base sum of normalised sales amounts
  - `Profit Margin %` — divide total profit margin by revenue with zero-division guard
  - `Revenue Contribution %` — each entity's share of total using `ALL()` to remove filter context
  - `Revenue Last Year` — `SAMEPERIODLASTYEAR()` for period-over-period comparison
  - `Target Diff` — actual profit margin % minus user-set profit target

  The `ALL()` function in contribution measures is critical: without it, Power BI would calculate a customer's share only within whatever filters are active, not against the true total. Every contribution percentage in the dashboard is accurate because of this.

**4. Dashboard** — KPI layer (₹142.22M revenue, 350K units, ₹2.1M profit), market analysis, time series trends, customer rankings, and product performance — all with slicer-driven interactivity.

**Key Business Insights Surfaced:**
- High revenue markets ≠ high-margin markets — profitability gaps are hidden in aggregated revenue figures
- Revenue concentration risk: a small number of customers drive the majority of sales
- Seasonal revenue patterns create planning opportunities for inventory and promotions

**Stack:** `MySQL` · `Power BI Desktop` · `DAX` · `Star Schema` · `Data Modeling`

---

### 🤖 [Image Conversational Chatbot](https://github.com/anmolzz-10/Image-conversational-chatbot)

> *A visual question-answering system: upload a car image, ask questions, get conversational answers — powered by BLIP-2 and Cohere.*

**The Idea:** Most chatbots accept text. This one accepts images. A user uploads a photograph of a vehicle and asks questions in natural language — "What model is this?", "What engine specifications does this car have?" — and receives a conversational, contextually aware response.

**How It Works:**

The system chains two AI models:

1. **BLIP-2 (Bootstrapping Language-Image Pre-training)** — A vision-language model that processes the uploaded image and generates a raw visual understanding: what objects are present, what the scene contains, what can be inferred about the vehicle.

2. **Cohere NLP API** — Takes BLIP-2's raw visual output and transforms it into a conversational, natural-language response that flows appropriately in a chat context. This two-model chain is what makes the bot feel like a conversation rather than a lookup.

**Technical Architecture:**
- **Flask** serves as the backend web framework, handling image uploads, session management, and API routing
- **PyTorch + CUDA** powers local BLIP-2 inference (GPU-accelerated for practical response times)
- **`model_save.ipynb`** handles downloading and serialising the BLIP-2 model weights from HuggingFace to local storage — eliminating download latency on every startup
- **HTML/CSS/JavaScript** frontend with single-page chat interface

**Why BLIP-2 over simpler OCR/classification approaches:** A classification model would identify a car model but couldn't answer open-ended questions. BLIP-2 is a generative vision-language model — it understands the image in context and can respond to arbitrary queries, not just predefined categories. This is the difference between a lookup table and genuine visual reasoning.

**Stack:** `Python` · `Flask` · `BLIP-2` · `Cohere API` · `PyTorch 2.5.1` · `CUDA 12.1` · `HTML/CSS/JS`

```
Flow:  Image Upload → BLIP-2 (Visual Understanding)
                   → Cohere (Conversational Refinement)
                   → Chat Response → Follow-up Questions
```

---

### 🧠 [End-to-End Machine Learning Project](https://github.com/anmolzz-10/ML-project)

> *A complete ML pipeline from EDA through model selection, training, evaluation, and cloud deployment on AWS Elastic Beanstalk.*

**What "End-to-End" Actually Means:**

Many ML projects stop at a trained model in a notebook. This one goes all the way to a deployed web application. The structure reflects real-world ML engineering, not just academic exploration:

```
notebook/         ← EDA and experimentation (the exploration phase)
src/              ← Modular, importable Python source code
  ├── components/ ← Data ingestion, transformation, model training
  ├── pipeline/   ← Predict pipeline (for serving) and train pipeline
  └── utils.py    ← Shared utilities
artifacts/        ← Serialised model and preprocessor objects
templates/        ← HTML for the Flask prediction interface
.ebextensions/    ← AWS Elastic Beanstalk deployment configuration
application.py    ← Entry point (named for EB compatibility)
setup.py          ← Package installation configuration
```

**The Pipeline Stages:**

**Data Ingestion** — Reads raw data and splits into train/test sets with reproducible random seeds. Saves artefacts for downstream stages.

**Data Transformation** — Separate preprocessing pipelines for numerical and categorical features using `sklearn.Pipeline`: imputation → scaling for numerics, imputation → encoding for categoricals. The fitted transformer is serialised to `artifacts/` so the exact same transformations apply at prediction time.

**Model Training** — Multiple algorithms are trained and evaluated systematically: Linear Regression, Ridge, Lasso, ElasticNet, Decision Tree, Random Forest, Gradient Boosting, XGBoost, CatBoost, AdaBoost. Hyperparameter grids are passed for each. The best-performing model is selected by R² score and serialised.

**CatBoost** is included specifically because it handles categorical features natively without pre-encoding — relevant when the dataset has high-cardinality categoricals where label encoding introduces arbitrary ordinal relationships.

**Prediction Pipeline** — A separate `PredictPipeline` class loads the serialised model and preprocessor, applies the same transformations to new inputs, and returns predictions. This separation between training and serving is essential for production deployment.

**Web Interface** — Flask serves a form-based interface where users input feature values and receive a prediction. The same `PredictPipeline` class handles inference.

**Deployment** — `.ebextensions/` contains the WSGI server configuration for AWS Elastic Beanstalk. `application.py` (not `app.py`) is the entry point name required by EB's detection logic.

**Stack:** `Python` · `Scikit-learn` · `XGBoost` · `CatBoost` · `Flask` · `AWS Elastic Beanstalk` · `Pandas` · `NumPy`

---

## 🛠️ Skills & Technologies

```
Analytics & BI          SQL (MySQL 8.0) · Power BI · DAX · Star Schema · Data Modeling
Python Data Stack       Pandas · NumPy · Scikit-learn · Plotly · Streamlit
Machine Learning        Linear/Ridge/Lasso Regression · Decision Trees · Random Forest
                        Gradient Boosting · XGBoost · CatBoost · AdaBoost
Deep Learning & AI      PyTorch · BLIP-2 · Cohere API · CUDA Acceleration
Web & Deployment        Flask · HTML/CSS/JS · AWS Elastic Beanstalk · Streamlit Cloud
SQL Advanced Concepts   UDFs · Stored Procedures · Views · CTEs · Window Functions
```

---

## 📐 How I Work

Every project here follows the same philosophy: **analysis should be reproducible, explainable, and decision-useful.**

That means:
- Writing SQL as infrastructure (functions, procedures, views) not just queries
- Separating training pipelines from serving pipelines in ML projects
- Documenting methodology for both technical and non-technical stakeholders
- Choosing interpretable models when the goal is explanation, not just prediction
- Deploying results so they're actually usable, not just sitting in a notebook

---

<div align="center">

*Data doesn't speak for itself — it needs someone to ask the right questions.*

[![Football Analytics](https://img.shields.io/badge/⚽_See_the_Live_App-Man_United_Analysis-DC143C?style=for-the-badge)](https://man-united-post-season-performance-analysis.streamlit.app/)

</div>
