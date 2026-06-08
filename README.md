## 📌 Executive Summary
The **Customer Sentiment & Loyalty Analytics Pipeline** is an automated, production-ready Natural Language Processing (NLP) and Business Intelligence (BI) workflow designed to process unstructured customer feedback. By extracting semantic context, assigning granular sentiment scores, and structuring this data for real-time relational analytics, this pipeline bridges the gap between raw textual feedback and actionable retention strategies. 

With this pipeline, marketing and loyalty retention teams transition from reactive firefighting to proactive engagement, leveraging a standardized **Brand Satisfaction Index (BSI)** to capture real-time market perception.

---

## 🚀 Objective & Business Impact
* **Automated NLP Ingestion:** Eliminated manual review auditing by engineering an asynchronous pipeline to ingest, parse, and analyze high-volume customer sentiment.
* **Data-Driven Retention:** Structured abstract qualitative text into distinct categorical trend metrics to identify specific churn triggers (e.g., service delays, pricing friction, product bugs).
* **Executive Visibility:** Empowered cross-functional stakeholders with dynamic BI dashboards that display immediate shifts in brand loyalty and customer experience health.

---

## 🛠️ Tech Stack & Architecture

The system utilizes a modern, cloud-native data stack designed for speed, relational integrity, and semantic depth:

* **Data Layer & Storage:** [Supabase](https://supabase.com/) (PostgreSQL) handles transactional records, user profiles, and structured analytical schemas, leveraging built-in security policy layers.
* **Orchestration & Processing:** [Python](https://www.python.org/) drives the ETL engine, managing text pre-processing, tokenization, API orchestration, and structured database upserts.
* **Semantic Inference Engine:** Advanced LLMs / Sentiment Retrieval Engines calculate fine-grained polarity scores, emotional vectors, and keyword extractions.
* **Visualization Layer:** BI Reporting Interfaces (e.g., Streamlit, Tableau, or Looker Studio) connected directly to Supabase views for zero-latency metric updates.

### System Architecture Flowchart

```

[Unstructured Data] ──> [Python ETL Engine] ──> [Semantic Retrieval Engine]
│
▼ (Vector/Polarity Mapping)
[BI Dashboards]    <──   [Supabase Database]  <─── [Structured SQL Mapping]

```

## 📊 Data Schema & Structured Logic

The pipeline transforms raw text strings into structured database entities. Below is the primary database schema implemented within Supabase:

```sql
-- Core Table for Storing Parsed Sentiment Records
CREATE TABLE customer_feedback_analytics (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    customer_id VARCHAR(100) NOT NULL,
    review_text TEXT NOT NULL,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    
    -- NLP Extraction Outputs
    sentiment_score NUMERIC(4,3), -- Ranges from -1.000 (Very Negative) to +1.000 (Very Positive)
    sentiment_category VARCHAR(20), -- 'Highly Positive', 'Positive', 'Neutral', 'Negative', 'Highly Negative'
    primary_topic VARCHAR(50),      -- e.g., 'Product Quality', 'Pricing', 'Customer Support'
    
    -- Loyalty & Retention Indicators
    churn_risk_index INT CHECK (churn_risk_index BETWEEN 1 AND 5),
    requires_escalation BOOLEAN DEFAULT FALSE
);

-- Indexing for High-Performance BI Queries
CREATE INDEX idx_sentiment_category ON customer_feedback_analytics(sentiment_category);
CREATE INDEX idx_primary_topic ON customer_feedback_analytics(primary_topic);

```

### Categorical Transformation Logic

To convert raw floats into explicit corporate KPIs, the `sentiment_score` is structured dynamically:

* `+0.500 to +1.000` ──> **Highly Positive** (Promoter / High Retention Loyalty)
* `+0.100 to +0.499` ──> **Positive** (Satisfied / Low Churn Risk)
* `-0.099 to +0.099` ──> **Neutral** (Passive)
* `-0.499 to -0.100` ──> **Negative** (At Churn Risk / Requires Monitoring)
* `-1.000 to -0.500` ──> **Highly Negative** (Critical Escalation / Customer Support Action Required)

---

## 📈 BI Reporting & Core Metrics

The parsed outputs are funneled into a semantic reporting interface that tracks the following key performance indicators:

1. **Brand Satisfaction Index (BSI):** A rolling 7-day weighted average of overall sentiment polarity, providing a macroeconomic health check of user sentiment.
2. **Loyalty Program Correlation:** Cross-referencing sentiment trends against loyalty tier distributions to identify if premium members face specific systematic friction.
3. **Categorical Trend Matrix:** Stacked bar charts and time-series heatmaps highlighting shifting issue topics over time, allowing marketing teams to detect adverse reactions to feature rollouts or pricing updates instantly.

---

## 🔧 Installation & Local Setup

### Prerequisites

* Python 3.10+
* Supabase Account & Project Credentials
* API keys for your preferred Semantic/LLM Engine

### Step-by-Step Installation

1. **Clone the repository:**
```bash
git clone [https://github.com/your-username/customer-sentiment-analytics-pipeline.git](https://github.com/your-username/customer-sentiment-analytics-pipeline.git)
cd customer-sentiment-analytics-pipeline

```


2. **Configure Environment Variables:**
Create a `.env` file in the root directory and populate your secrets:
```env
SUPABASE_URL=[https://your-project-id.supabase.co](https://your-project-id.supabase.co)
SUPABASE_SERVICE_ROLE_KEY=your-supabase-service-role-key
SEMANTIC_ENGINE_API_KEY=your-api-key-here

```


3. **Install Dependencies:**
```bash
pip install -r requirements.txt

```


4. **Initialize Database Schema:**
Execute the SQL statements provided in the `schema.sql` file within your Supabase SQL Editor to spin up the indexed analytical tables and analytical views.
5. **Run the Pipeline Engine:**
```bash
python src/main.py

```



---

## 👥 Contributors & Feedback

For architectural questions, data pipeline enhancement proposals, or BI configuration requests, please contact the Analytics Engineering and Marketing Ops Core Teams.

