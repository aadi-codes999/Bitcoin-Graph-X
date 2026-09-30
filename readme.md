'''Project Architecture'''
                    ┌─────────────────────────┐
                    │ Synthetic Input Dataset │
                    │ CSV / JSON / XML         │
                    └────────────┬────────────┘
                                 │
                                 ▼
                    ┌─────────────────────────┐
                    │  Data Ingestion Layer    │
                    │ • Parser                 │
                    │ • Validation             │
                    │ • Deduplication          │
                    └────────────┬────────────┘
                                 │
                                 ▼
              ┌────────────────────────────────────┐
              │      Correlation & Enrichment      │
              │                                    │
              │ IP ↔ TXID ↔ Wallet ↔ Timestamp    │
              │ IP → Country / ASN                 │
              └────────────────┬───────────────────┘
                               │
                 ┌─────────────┴──────────────┐
                 ▼                            ▼
       ┌──────────────────┐         ┌──────────────────┐
       │ Feature Engine   │         │ Graph Builder    │
       │                  │         │                  │
       │ amount features  │         │ IP nodes         │
       │ timing features  │         │ Wallet nodes     │
       │ frequency        │         │ TX nodes         │
       │ degree           │         │ edges            │
       │ velocity         │         │ temporal links   │
       └────────┬─────────┘         └────────┬─────────┘
                │                            │
                ▼                            ▼
       ┌──────────────────┐         ┌──────────────────┐
       │ AI/ML Detection  │         │ Entity Clustering│
       │                  │         │                  │
       │ Isolation Forest │         │ Node2Vec         │
       │ / XGBoost        │         │ + HDBSCAN        │
       └────────┬─────────┘         └────────┬─────────┘
                │                            │
                └────────────┬───────────────┘
                             ▼
                 ┌─────────────────────────┐
                 │ Explainable Risk Engine │
                 │                         │
                 │ Risk Score              │
                 │ Evidence                │
                 │ ML explanation          │
                 │ Confidence              │
                 └────────────┬────────────┘
                              │
                              ▼
                 ┌─────────────────────────┐
                 │ Investigator Dashboard  │
                 │                         │
                 │ Alerts                  │
                 │ Graph visualization     │
                 │ Timeline                │
                 │ Evidence panel          │
                 └─────────────────────────┘


'''Repo Structure'''


bitcoingraph-x/
│
├── data/
│   ├── raw/
│   ├── processed/
│   └── synthetic/
│
├── geoip/
│   ├── GeoLite2-Country.mmdb
│   └── GeoLite2-ASN.mmdb
│
├── src/
│   ├── ingestion/
│   │   ├── csv_parser.py
│   │   ├── json_parser.py
│   │   └── xml_parser.py
│   │
│   ├── preprocessing/
│   │   ├── normalize.py
│   │   └── validate.py
│   │
│   ├── enrichment/
│   │   └── geoip.py
│   │
│   ├── graph/
│   │   ├── builder.py
│   │   ├── features.py
│   │   └── embeddings.py
│   │
│   ├── ml/
│   │   ├── anomaly.py
│   │   ├── clustering.py
│   │   └── explain.py
│   │
│   ├── scoring/
│   │   └── risk_engine.py
│   │
│   └── generator/
│       └── synthetic_data.py
│
├── dashboard/
│   └── app.py
│
├── models/
│   └── model.pkl
│
├── tests/
│
├── requirements.txt
├── README.md
└── run.sh
