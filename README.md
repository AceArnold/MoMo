# MoMo SMS Analytics — Team Repo

> Process MoMo SMS data in XML, clean & categorize it, store in SQLite, and visualize insights on a simple dashboard.

## 👥 Team
- Team name: **YOUR_TEAM_NAME**
- Members: Add names + GitHub usernames here

## 🚀 Project Overview
Pipeline:
1) **Parse** raw XML MoMo SMS
2) **Clean & normalize** amounts, dates, and phone numbers
3) **Categorize** transactions (e.g., cash-in, cash-out, fees, airtime, merchant, P2P)
4) **Load** into SQLite
5) **Export aggregates** to `data/processed/dashboard.json`
6) **Frontend** (static) renders charts & tables from the JSON

## 🧱 Architecture (Mermaid)
```mermaid
flowchart LR
  A[Raw MoMo XML (data/raw/momo.xml)] --> B[ETL: parse_xml.py]
  B --> C[clean_normalize.py]
  C --> D[categorize.py]
  D --> E[load_db.py (SQLite)]
  E --> F[export JSON (run.py)]
  F --> G[Frontend: index.html + chart_handler.js]
  subgraph Data
    A
    F[data/processed/dashboard.json]
    E[(data/db.sqlite3)]
  end
```
> If you prefer Draw.io or Miro, create your diagram and paste the share link here: **ARCHITECTURE_DIAGRAM_LINK**

## 📋 Scrum Board
Add your board link here (GitHub Projects, Trello, or Jira): **SCRUM_BOARD_LINK**  
Columns: **To Do**, **In Progress**, **Done**. Seed tasks are included below.

### Suggested Initial Tasks
- Repo setup and collaborators
- Architecture diagram
- Define data model (tables, fields)
- Implement parser
- Implement cleaners (amount/date/phone)
- Categorization rules
- SQLite load & upsert
- Export dashboard aggregates
- Frontend data fetch + charts
- Unit tests
- CI (optional)

## 🛠️ Getting Started

### 0) Python & virtualenv
```bash
python3 -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate
pip install -r requirements.txt
cp .env.example .env
```

### 1) Put your MoMo XML
Place the raw MoMo XML as `data/raw/momo.xml` (this path is .gitignored).

### 2) Run ETL
```bash
bash scripts/run_etl.sh
# or
python etl/run.py --xml data/raw/momo.xml
```

### 3) Serve Frontend
```bash
bash scripts/serve_frontend.sh
# then open http://localhost:8000
```

### 4) Rebuild Dashboard JSON
```bash
bash scripts/export_json.sh
```

## 🧪 Tests
```bash
pytest -q
```

## 🗂️ Project Tree
```
.
├── README.md
├── .env.example
├── requirements.txt
├── index.html
├── web/
│   ├── styles.css
│   └── chart_handler.js
├── data/
│   ├── raw/                  # (git-ignored)
│   ├── processed/
│   │   └── dashboard.json
│   ├── db.sqlite3
│   └── logs/
│       ├── etl.log
│       └── dead_letter/
├── etl/
│   ├── __init__.py
│   ├── config.py
│   ├── parse_xml.py
│   ├── clean_normalize.py
│   ├── categorize.py
│   ├── load_db.py
│   └── run.py
├── api/                      # (optional bonus)
│   ├── __init__.py
│   ├── app.py
│   ├── db.py
│   └── schemas.py
├── scripts/
│   ├── run_etl.sh
│   ├── export_json.sh
│   └── serve_frontend.sh
└── tests/
    ├── test_parse_xml.py
    ├── test_clean_normalize.py
    └── test_categorize.py
```

## 📄 License
MIT (or your choice)
