# Self-Healing Data Pipeline for Sentiment Analysis

A **production-ready, AI-powered data pipeline** that automatically **detects, heals, and reports data quality issues** during sentiment analysis of Yelp reviews.  
The pipeline is orchestrated using **Apache Airflow** and leverages **LLM-powered reasoning via Ollama** to ensure resilient, reliable data processing.

---

## 🚀 Key Features

- Automated **sentiment analysis** on Yelp review data
- Built-in **self-healing logic** for common data quality failures
- **LLM-assisted validation and recovery**
- End-to-end orchestration using **Apache Airflow**
- Detailed **health reports and metrics** for observability
- Timestamped outputs for auditability and traceability

---

## 🏗️ Architecture

![Self healing pipeline](https://github.com/user-attachments/assets/87aa3e2e-7dfa-4d87-87f0-bc8908433d17)

**High-level flow:**

1. Data ingestion from Yelp review source
2. Data quality validation layer
3. Automated healing of invalid records
4. Sentiment analysis using LLM
5. Metrics aggregation and health reporting
6. Persisted outputs with run metadata

---

## 🧠 Self-Healing Capabilities

The pipeline automatically detects and heals the following data quality issues **without manual intervention**:

| Error Type | Detection Logic | Healing Action |
|----------|----------------|----------------|
| `missing_text` | Text field is `None` | Fill with placeholder |
| `empty_text` | Text is empty or whitespace | Fill with placeholder |
| `wrong_type` | Text is not a string | Type conversion |
| `special_characters_only` | No alphanumeric characters | Replace with marker |
| `too_long` | Exceeds max length (2000 chars) | Truncate with ellipsis |

---

## 📊 Sample Health Report

Each pipeline run generates a structured health report summarizing quality, recovery, and sentiment outcomes:

```json
{
  "pipeline": "self_healing_pipeline",
  "health_status": "HEALTHY",
  "metrics": {
    "total_processed": 100,
    "success_rate": 0.85,
    "healing_rate": 0.15,
    "degradation_rate": 0.0
  },
  "sentiment_distribution": {
    "POSITIVE": 45,
    "NEGATIVE": 30,
    "NEUTRAL": 25
  }
}

📦 Output Artifacts
Output Location

Results are saved under the output/ directory with timestamped filenames for traceability:

output/
└── sentiment_analysis_summary_2025-12-08_14-30-00_Offset0.json

Output Schema

```json
{
  "run_info": {
    "timestamp": "2025-12-08T14:30:00",
    "batch_size": 100,
    "offset": 0
  },
  "totals": {
    "processed": 100,
    "success": 85,
    "healed": 15,
    "degraded": 0
  },
  "rates": {
    "success_rate": 0.85,
    "healing_rate": 0.15,
    "degradation_rate": 0.0
  },
  "sentiment_distribution": {
    "POSITIVE": 45,
    "NEGATIVE": 30,
    "NEUTRAL": 25
  },
  "healing_statistics": {...},
  "results": [...]
}
