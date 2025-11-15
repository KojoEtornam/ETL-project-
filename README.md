# 🌦️ Weather Data Engineering Pipelines (Airflow ETL)

This project contains a collection of **Weather ETL Pipelines** built with **Python** and orchestrated using **Apache Airflow**.  
It demonstrates real-world Data Engineering concepts including:

- API ingestion (OpenWeatherMap)
- ETL (Extract → Transform → Load)
- Airflow DAG scheduling
- SQLite data warehousing (local)
- Data normalization with pandas
- Modular, multi-pipeline architecture

This is one unified project containing **multiple pipelines**, each performing different ETL tasks.

---

# 📁 Project Pipelines

### 1️⃣ **Hourly Weather ETL (Accra)**
Fetches **current weather for Accra every hour**, transforms it, and stores it in SQLite.

**Use cases:** trend analysis, dashboards, monitoring.

### 2️⃣ **Multi-City Weather ETL**
Fetches weather for **Accra, Kumasi, London, New York** every few hours and saves them together for comparison.

**Use cases:** cross-city analytics, multi-location monitoring.

### 3️⃣ **Historical Weather ETL**
Loads historical weather data (API/CSV), cleans it, and stores it in SQLite for ML and forecasting.

**Use cases:** machine learning pipelines, forecasting, analytics, time-series modeling.

---

# 🧱 Tech Stack

| Component | Usage |
|----------|-------|
| **Python** | Core ETL logic |
| **Apache Airflow 2.x** | DAG scheduling & orchestration |
| **Requests** | API consumption |
| **Pandas** | Data transformations |
| **SQLite** | Local database (simple warehouse) |
| **Docker (optional)** | Airflow containerization |
| **Environment Variables** | Secure API key handling |

---

# 🔧 Project Structure

```
weather-etl/
├── dags/
│   ├── multicity_weather_etl.py
│   ├── weather_hourly_etl.py
│   └── historical_weather_etl.py
├── data/
│   └── (SQLite databases stored here)       # Gitignored
├── README.md
├── requirements.txt
└── .gitignore
```

---

# ⚙️ Installation & Setup

### 1️⃣ Clone Repository
```bash
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>
```

### 2️⃣ Create Virtual Environment
```bash
python -m venv venv
source venv/bin/activate      # Linux / Mac
venv\Scripts\activate         # Windows
```

### 3️⃣ Install Dependencies
```bash
pip install -r requirements.txt
```

### 4️⃣ Set Environment Variables
Create a `.env` or export directly:

```bash
export OPENWEATHER_API_KEY="your_api_key"
export WEATHER_DB_PATH="./data/weather.db"
```

Never hardcode API keys.

---

# 🚀 Running the Pipelines

## **▶️ Option A — Run in Airflow (Recommended)**

### Start Airflow locally:
```bash
airflow db init
airflow webserver -p 8080
airflow scheduler
```

Copy your DAGs into Airflow's `dags/` directory:

```
~/airflow/dags/
```

Then go to:

🔗 **http://localhost:8080**

Enable and trigger your DAGs.

---

## **▶️ Option B — Run ETL Logic Locally (Without Airflow)**

You can manually execute the pipelines for testing.

Example:
```python
from multicity_weather_etl import extract, transform, load

raw = extract()
clean = transform(data=raw)   # adjust signature for local testing
load(records=clean)
```

Useful for debugging transformation or DB issues.

---

# 🗄️ Database Schema

All ETL pipelines load into a `weather` table containing:

| Column | Description |
|--------|-------------|
| city | City name |
| temperature | Temperature (°C) |
| humidity | Humidity % |
| weather | Description text |
| wind_speed | Wind speed (m/s) |
| timestamp | UTC timestamp |

---

# 🔐 Security Best Practices

- Store API keys in **environment variables**  
- Add `.env` to **.gitignore**  
- Do NOT store SQLite DB in GitHub  
- Use **PostgreSQL** / Snowflake / BigQuery for production workloads  
- Add Airflow secrets backend for sensitive credentials  

---

# 📈 Future Improvements (Data Engineering Roadmap)

| Area | Possible Upgrade |
|------|------------------|
| Storage | Move from SQLite → PostgreSQL |
| Raw Zone | Add S3/GCS cloud storage bucket |
| Transformation | Add dbt models |
| Monitoring | Add Airflow alerts / Grafana |
| ML | Build predictive weather model |
| Tests | Add pytest for the transform step |

---

# 🧪 Testing

You can add unit tests under:

```
tests/
```

Example test (pytest):
```python
def test_transform():
    sample = {...}
    output = transform(data=[sample])
    assert "temperature" in output[0]
```

---

# 📦 Requirements

```
apache-airflow>=2.3.0
pandas>=1.4.0
requests>=2.28.0
python-dotenv>=0.21.0
```

---

# ✨ Author

**John Botsyoe Etornam**  
Data Engineering • Mobile Development • Cloud • Python  
GitHub: https://github.com/KojoEtornam  
LinkedIn: John (BOTSYOE) Etornam

---

