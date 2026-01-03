# Phone Call Behaviour Analysis

Analyzing ~25,000 outgoing calls from a South African business owner's wife (Jan 2022 - Oct 2024). The objective: classify 1,977 "Unknown" contacts and identify any suspicious calling patterns.

## Key Findings

**Classification of Unknown Contacts:**
| Category | Count | % |
|----------|-------|---|
| Service Provider | 958 | 48.5% |
| Supplier | 898 | 45.4% |
| Important Contacts | 97 | 4.9% |
| Family | 24 | 1.2% |

93.9% of Unknown contacts are business-related. The "Unknown" category was mostly unlabeled business contacts, not hidden personal relationships.

**Suspicious Contacts Identified:**
- **Duma** - 210 calls, 27 late-night (1-5 AM), 30-min call at 5 AM, ended Nov 2022
- **Eric** - 219 calls, 9 late-night (9-11 PM), 25-min call at 11 PM Friday, ongoing
- **Modiba** - 27 calls, 97-min max call, peak hour 8 PM, ongoing (found via clustering)

## Project Structure

```
├── data/
│   ├── raw/                    # Original Kaggle dataset
│   ├── processed/              # Cleaned call-level data
│   └── features/               # Contact-level features + predictions
├── notebooks/
│   ├── 01_data_cleaning.ipynb
│   ├── 02_data_exploration.ipynb
│   ├── 03_feature_engineering.ipynb
│   ├── 04_supervised_learning.ipynb
│   ├── 05_clustering.ipynb
│   └── 06_business_insights.ipynb
├── config/
│   └── config.yaml             # Business hours definition
└── reports/
    ├── figures/
    └── findings/
```

## Notebooks

| # | Notebook | Description |
|---|----------|-------------|
| 01 | Data Cleaning | Load raw data, fix column names, add hour and business hours flags |
| 02 | Data Exploration | EDA, category patterns, identify suspicious "muffens" (Duma, Eric) |
| 03 | Feature Engineering | Create 14 contact-level features from call-level data |
| 04 | Supervised Learning | RandomForest classifier (79% accuracy), predict Unknown categories |
| 05 | Clustering | K-Means (K=5) on Unknown contacts, discover Modiba as new suspect |
| 06 | Business Insights | Final report with visualizations and conclusions |

## Methods

**Supervised Learning:**
- RandomForest trained on 114 labeled contacts
- 9 behavioral features (duration, timing, frequency)
- 79% test accuracy
- Applied to predict 1,977 Unknown contacts

**Unsupervised Learning:**
- K-Means clustering (K=5) on Unknown contacts
- Identified 5 behavioral clusters
- Cluster 4 ("Heavy Talkers") contained suspicious contacts with unusually long calls

## Setup

```bash
pip install -r requirements.txt
cd notebooks
jupyter notebook
```

Run notebooks in order (01 → 06).

## Data

Source: [Kaggle - Semi-Categorized Phone Dataset](https://www.kaggle.com/)

- 24,952 calls
- 2,091 unique contacts
- 5 categories: Family, Supplier, Service Provider, Important Contacts, Unknown

## Output

Final classified dataset: `data/features/contacts_final.csv`

Columns:
- `name` - Contact identifier
- `category` - Original label
- `predicted_category` - Model prediction for Unknown contacts
- `final_category` - Original if labeled, prediction if Unknown
- 14 behavioral features
