# 🚢 MARIVANCE : AI-Powered Maritime Decision Intelligence DSS
### Autonomous Maritime Freight Forecasting, Port Feasibility & Fleet Chartering Optimizer
**Smart India Hackathon (SIH 2026) • Problem Statement ID: PS 26006**  
**Ministry of Steel, Government of India • Steel Authority of India Limited (SAIL) & RINL**

---

[![Node.js](https://img.shields.io/badge/Node.js-18+-339933?style=for-the-badge&logo=node.js&logoColor=white)](https://nodejs.org/)
[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![React](https://img.shields.io/badge/React-18.3-61DAFB?style=for-the-badge&logo=react&logoColor=black)](https://react.dev/)
[![Vite](https://img.shields.io/badge/Vite-5.4-646CFF?style=for-the-badge&logo=vite&logoColor=white)](https://vitejs.dev/)
[![XGBoost](https://img.shields.io/badge/XGBoost-v2.0-EB4034?style=for-the-badge)](https://xgboost.readthedocs.io/)
[![PuLP MILP](https://img.shields.io/badge/PuLP-MILP%20Solver-2C3E50?style=for-the-badge)](https://coin-or.github.io/pulp/)
[![Three.js](https://img.shields.io/badge/Three.js-WebGL-000000?style=for-the-badge&logo=three.js&logoColor=white)](https://threejs.org/)
[![License](https://img.shields.io/badge/License-Proprietary%20%2F%20MoS-orange?style=for-the-badge)]()

---

## 📌 Executive Overview

India's domestic steel industry depends heavily on imported coking coal to feed blast furnaces across major public-sector plants (**Bhilai, Bokaro, Rourkela, Durgapur, IISCO Burnpur, and Visakhapatnam Steel Plant**). Every year, **Steel Authority of India Limited (SAIL)** and **RINL** import millions of metric tonnes of metallurgical coking coal from global origins, including **Australia (Hay Point, Newcastle), the United States (Hampton Roads, Baltimore), South Africa (Richards Bay), Mozambique (Nacala), Indonesia (Kalimantan, Taboneo), and Russia (Taman, Vostochny)**.

However, maritime chartering and logistics execution face severe structural hurdles:
1. **Volatile Ocean Freight Markets:** Spot rates swing wildly based on Baltic Dry Index (BDI), bunker fuel prices (VLSFO), geopolitical shocks, and seasonal monsoons.
2. **Physical Draft & Berth Restrictions:** Shallow riverine ports like **Haldia** (~8.5 m draft) cannot accommodate Capesize or fully laden Panamax vessels, causing severe tidal grounding risks or forced offshore lightering.
3. **Severe Port Demurrage Penalties:** Congestion at major ports (average queues of 4.5–4.8 days at Paradip and Haldia) generates millions of dollars in demurrage liabilities ($15,000–$36,000/day charter party penalties).
4. **Sub-optimal Fleet Allocation:** Manually deciding vessel splits (Handysize vs. Supramax vs. Panamax vs. Capesize) often leads to lost economies of scale or draft non-compliance.

**MARIVANCE** is an end-to-end, enterprise-grade **Maritime Decision Support System (DSS)** that unifies **machine learning rate forecasting (XGBoost)**, **physical waterline constraint validation**, **Mixed-Integer Linear Programming (MILP) fleet optimization**, **demurrage risk mitigation**, and **generative AI logistics advisory** into a unified command dashboard.

---

## 🏛️ Core Pillars of Intelligence

```
                                  ┌────────────────────────────────────────────────────────┐
                                  │           MARIVANCE Command & Decision Hub             │
                                  └────────────────────────────────────────────────────────┘
                                                               │
         ┌─────────────────────────┬───────────────────────────┼───────────────────────────┬─────────────────────────┐
         ▼                         ▼                           ▼                           ▼                         ▼
┌──────────────────┐      ┌──────────────────┐      ┌──────────────────┐      ┌──────────────────┐      ┌──────────────────┐
│  Pillar 1: ML    │      │ Pillar 2: Water- │      │  Pillar 3: MILP  │      │ Pillar 4: Demur- │      │ Pillar 5: GenAI  │
│  Rate Forecast   │      │ line Feasibility │      │ Fleet Optimizer  │      │ rage Mitigation  │      │ Logistics Copilot│
├──────────────────┤      ├──────────────────┤      ├──────────────────┤      ├──────────────────┤      ├──────────────────┤
│ • XGBoost Regr.  │      │ • Draft & LOA    │      │ • PuLP Optimizer │      │ • Laytime engine │      │ • Grounded LLM   │
│ • 7-day Lags     │      │ • Tidal windows  │      │ • Capesize/Panam │      │ • Port wait data │      │ • Maritime RAG   │
│ • BDI + VLSFO    │      │ • UKC validation │      │ • Cost min. obj. │      │ • Diversion ROI  │      │ • SAIL domain KB │
│ • R² = 92.01%    │      │ • Haldia barrier │      │ • Integer splits │      │ • $78k/vessel sv │      │ • Instant triage │
└──────────────────┘      └──────────────────┘      └──────────────────┘      └──────────────────┘      └──────────────────┘
```

### 1. 📈 Machine Learning Rate Forecasting Engine
- **Model Architecture:** Custom `XGBoost Regressor` trained on multi-year longitudinal coking coal freight records (2021–2025).
- **Exogenous Signals:** Baltic Dry Index (BDI), Very Low Sulphur Fuel Oil (VLSFO) prices with 7-day lagged sliding windows, global coal pricing, monsoon seasonality flags, and origin-destination nautical mile distances.
- **Accuracy Benchmarks:**
  - **Test $R^2$ Score:** `0.9201` (vs. Baseline Linear Regression `0.8991`)
  - **Test RMSE:** `3.26 USD/MT` (an **11.02%** precision gain over baseline)
  - **Test MAE:** `2.56 USD/MT`
  - **Top Feature Contributors:** Voyage distance (nautical miles), origin routing, monsoon seasonality, and BDI momentum.

### 2. 🌊 Waterline Physical Feasibility Engine
- Rigorous mathematical validation of vessel geometry against discharge port infrastructure:
  $$\text{Draft}_{\text{vessel}} \le \text{Draft}_{\text{port}} - \text{UKC}_{\text{min}}$$
- Pre-loaded with official maritime parameters:
  - **Gangavaram:** Draft $18.2\,\text{m}$, LOA $300\,\text{m}$ (Ultra-deepwater, Capesize accessible)
  - **Dhamra:** Draft $18.0\,\text{m}$, LOA $290\,\text{m}$ (Deepwater bulk)
  - **Paradip:** Draft $16.5\,\text{m}$, LOA $260\,\text{m}$ (Capesize/Panamax, tidal restrictions)
  - **Visakhapatnam (Vizag):** Draft $14.5\,\text{m}$, LOA $240\,\text{m}$ (Panamax limit)
  - **Gopalpur:** Draft $14.5\,\text{m}$, LOA $230\,\text{m}$ (Panamax all-weather)
  - **Haldia:** Draft $8.5\,\text{m}$, LOA $190\,\text{m}$ (Severe riverine tidal constraint; Handysize only)

### 3. ⚙️ Prescriptive MILP Fleet Chartering Optimizer
- Formulated as a **Mixed-Integer Linear Program (MILP)** solved via `PuLP`:
  $$\min \sum_{v \in V} \left( \text{CharterCost}_v \cdot x_v + \text{LaytimePenalty}_v \cdot x_v \right)$$
  $$\text{subject to} \quad \sum_{v \in V} \text{Capacity}_v \cdot x_v \ge \text{TargetDemand}$$
  $$x_v \in \mathbb{Z}_{\ge 0}, \quad \text{Feasibility}(v, \text{Port}) = 1$$
- Automatically recommends the optimal vessel mix (e.g., $2 \times \text{Panamax}$ vs. $1 \times \text{Capesize}$) to maximize scale discounts while preventing port draft lockouts.

### 4. ⏱️ Demurrage Exposure Quantification & Strategic Diversion
- Live laytime calculation balancing contractual allowed laytime against actual berth wait times and discharge rates:
  $$\text{Allowed Laytime} = \frac{\text{Cargo Volume}}{\text{Charterparty Laytime Rate (MT/Day)}}$$
  $$\text{Excess Stay} = \max\left(0, \, \text{Port Congestion} + \frac{\text{Cargo Volume}}{\text{Port Discharge Rate}} - \text{Allowed Laytime}\right)$$
  $$\text{Demurrage Liability} = \text{Excess Stay} \times \text{Daily Charter Demurrage Rate}$$
- **Automated Diversion Modeling:** Evaluates redirecting congested tonnage (e.g., Paradip $4.8\,\text{days}$ queue) to Gangavaram ($1.1\,\text{days}$ queue), generating documented net savings of up to **$78,000 per voyage**.

### 5. 🤖 Grounded Maritime Logistics Copilot
- Intelligent domain-specialized copilot powered by LLM integration (`google-generativeai`) with a grounded fallback knowledge engine.
- Instant explanations for chartering rationale, lightering procedures at Sandheads, Russian Far-East coal arbitrage (Vostochny vs. Hay Point), and railway rake coordination to SAIL steel plants.

---

## 💻 System Architecture & UI Modalities

MARIVANCE offers two coordinated frontend portals backed by a resilient API:

| Interface | Technology | Primary Audience | Key Capabilities |
| :--- | :--- | :--- | :--- |
| **Executive Landing Portal** | React 18, Vite, Three.js, Lucide Icons | Ministry Leadership, Directors, Commercial Heads | 3D Interactive Vessel Canvas, Core Pillars, Port Matrix, Strategic Impact, Secure Sign-In |
| **Operational DSS Dashboard** | Vanilla JS, HTML5, Plotly.js, Chart.js, Canvas | Freight Officers, Logistics Planners, Charterers | Live Route Simulator, Waterline Visualizer, MILP Fleet Solver, Congestion Radar, AI Copilot |
| **Data Science Studio** | Python Streamlit, Plotly, SQLAlchemy | Quant Analysts, Data Scientists | Longitudinal EDA, Model Retraining, Sensitivity Analysis, Raw Metric Inspection |
| **Backend REST API** | Node.js, Express, CORS | System Integration | `/api/simulate`, `/api/telemetry`, `/api/ports`, `/api/copilot`, `/api/health` |

---

## 🗂️ Repository Directory Structure

```plaintext
ocean_iq/
├── .gitignore                                # Git ignore rules
├── coking_coal_freight_rates_2021_2025.csv   # Historical freight dataset (7,272 records)
├── port_constraints.csv                     # Indian discharge port specifications
├── logistics_platform.db                     # SQLite operational database
├── freight_xgboost_model.pkl                 # Trained XGBoost regression model artifact
├── model_features.pkl                        # Model feature schema artifact
├── metrics.json                              # Machine learning evaluation metrics
├── db_setup.py                               # SQLite DB setup & CSV ingestion script
├── train_forecast_model.py                   # Model training & lag-feature engineering
├── optimization_engine.py                    # Standalone PuLP MILP solver script
├── dashboard.py                              # Streamlit executive command dashboard
├── server.js                                 # Express.js REST API server (Port 5000)
├── package.json                              # Node dependencies and scripts
├── requirements.txt                          # Python dependencies
├── vite.config.js                            # Vite dev server configuration
├── world_110m.json                           # GeoJSON world topology for route maps
│
├── public/                                   # Operational DSS Web Application
│   ├── main_dashboard.html                   # Command center single-page dashboard
│   ├── dashboard_logic.js                    # Reactive state, simulation & API logic
│   ├── dashboard_styles.css                  # High-density dark glassmorphism stylesheet
│   ├── maritime_routes.js                    # Orthodromic shipping route geometry
│   ├── plotly.min.js                         # Local Plotly distribution
│   └── hero-background.svg                  # SVG assets
│
├── src/                                      # React 18 Executive Landing Page
│   ├── App.jsx                               # Root application component
│   ├── main.jsx                              # Entrypoint
│   ├── index.css                             # Global design system & theme variables
│   └── components/                           # Modular UI components
│       ├── Navbar.jsx                        # Header with Ministry seal & Login modal
│       ├── Hero.jsx                          # 3D interactive hero section
│       ├── Pillars.jsx                       # 5-Pillar intelligence breakdown
│       ├── PortMatrix.jsx                    # Discharge port capability matrix
│       ├── ImpactSection.jsx                 # Quantified cost savings metrics
│       └── Footer.jsx                        # Regulatory & copyright footer
│
└── utils/                                    # Python Backend Utilities
    ├── __init__.py                           # Package initialization
    ├── predictor.py                          # Freight rate inference wrapper
    ├── feasibility.py                        # Physical port waterline validation
    ├── optimizer.py                          # PuLP optimization routines
    └── copilot_engine.py                     # AI Copilot knowledge base & LLM wrapper
```

---

## 📊 Machine Learning Model Benchmarks

Model training was conducted on 7,272 real-world records covering coking coal shipping trades into Indian ports between 2021 and 2025.

```
                    Model Performance Comparison (Test Set)
  100% ┌────────────────────────────────────────────────────────┐
       │                                            ████████ 92.01%
   90% │  ████████ 89.91%                           ████████    │
       │  ████████                                  ████████    │
       │  ████████                                  ████████    │
       │  Linear Regression Baseline                XGBoost Regressor
       └────────────────────────────────────────────────────────┘
```

| Metric | Linear Regression Baseline | MARIVANCE XGBoost Engine | Relative Gain |
| :--- | :--- | :--- | :--- |
| **$R^2$ Score (Accuracy)** | `0.8991` (89.9%) | **`0.9201` (92.0%)** | **+2.1% Absolute** |
| **Root Mean Squared Error (RMSE)** | `$3.67 / MT` | **`$3.26 / MT`** | **11.02% Error Reduction** |
| **Mean Absolute Error (MAE)** | `$2.86 / MT` | **`$2.56 / MT`** | **10.60% Error Reduction** |
| **Training Records / Splits** | 80% Train (5,817) | 20% Test (1,455) | 18 Engineered Features |

### Top Predictive Feature Importances
1. **Origin Distance (`distance_nm` & Baltimore/Kalimantan)** — 71.4% combined weight
2. **Monsoon Seasonality Flag (`is_monsoon`)** — 4.15% weight
3. **Baltic Dry Index (`bdi_index`)** — 3.25% weight
4. **Coking Coal Benchmark (`coal_price_usd`)** — 2.25% weight
5. **VLSFO Bunker Fuel (`vlsfo_price` & `vlsfo_price_lag7`)** — 0.89% weight

---

## 🚀 Installation & Getting Started

### 1. Prerequisites
- **Node.js** (v18.0.0 or higher) & **npm**
- **Python** (v3.10 or higher) & **pip**
- **Git**

### 2. Clone the Repository
```bash
git clone https://github.com/hritvikrajmishra/MARIVANCE_Maritime_DSS_Project.git
cd MARIVANCE_Maritime_DSS_Project
```

### 3. Python Environment Setup
```bash
# Create and activate a virtual environment
python -m venv venv

# Windows (PowerShell):
.\venv\Scripts\Activate.ps1

# Linux / macOS:
source venv/bin/activate

# Install Python requirements
pip install -r requirements.txt
```

### 4. Database Setup & Model Verification
The repository includes pre-built database and model artifacts. To re-ingest or retrain:
```bash
# Ingest CSV datasets into SQLite
python db_setup.py

# Train XGBoost model and generate metrics.json
python train_forecast_model.py
```

### 5. Node.js Full-Stack App Setup
```bash
# Install frontend & server dependencies
npm install

# Launch Full-Stack Concurrent Server (Express API + Vite Dev Server)
npm run dev
```

The services will start at:
- **Executive React Portal:** `http://localhost:3000` (or `http://localhost:5173`)
- **Operational Command Center (DSS):** `http://localhost:5000/main_dashboard.html` (Accessible via "Enter Command Center" button on the portal)
- **Express Backend API:** `http://localhost:5000`

### 6. (Optional) Run the Streamlit Command Center
```bash
streamlit run dashboard.py
```
Accessible at: `http://localhost:8501`

---

## 📡 REST API Reference

The Express.js server (`server.js`) exposes core simulation and telemetry endpoints:

### 1. `GET /api/health`
Returns health check, model architecture, and engine status.
```json
{
  "status": "online",
  "engine": "MARIVANCE : AI-Powered Maritime Decision Intelligence Engine",
  "ml_pipeline": "XGBoost v2.0 (R²=92.01%)",
  "optimizer": "PuLP MILP Solver"
}
```

### 2. `GET /api/ports`
Returns ground-truth port constraints, candidate origins, and vessel geometry specs.

### 3. `GET /api/telemetry`
Returns active market indexes including Baltic Dry Index (BDI), Capesize TC rates, Panamax 4TC, VLSFO bunker rates, and port turnaround days.

### 4. `POST /api/simulate`
Simulates a voyage and computes landed freight cost, vessel feasibility, and demurrage exposure.
- **Request Body:**
  ```json
  {
    "origin": "Hay Point (Australia)",
    "destination": "Paradip",
    "cargoVolume": 150000,
    "contractType": "Spot"
  }
  ```
- **Response:**
  ```json
  {
    "origin": "Hay Point (Australia)",
    "destination": "Paradip",
    "distanceNm": 4900,
    "effectiveRateUsd": 28.32,
    "totalOceanCostUsd": 4248000,
    "feasibleVessel": "Capesize",
    "vesselCount": 1,
    "fleetSummary": "1x Capesize",
    "feasibilityStatus": "optimal",
    "demurrageExposureUsd": 86400,
    "gangavaramDiversionSavingsUsd": 78200
  }
  ```

### 5. `POST /api/copilot`
Submits natural language queries to the grounded maritime intelligence copilot.
- **Request Body:** `{"queryKey": "panamax_vs_cape"}` or `{"customPrompt": "Why is Haldia restricted?"}`

---

## 🛳️ Vessel Class Reference Matrix

| Class | Deadweight (DWT / Capacity) | Loaded Draft | Length Overall (LOA) | Scale Freight Discount | Daily Charter / Demurrage Benchmark |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Handysize** | $35,000\,\text{MT}$ | $8.5\,\text{m}$ | $180\,\text{m}$ | $0\%$ (Baseline) | $\approx \$15,000 / \text{day}$ |
| **Supramax** | $55,000\,\text{MT}$ | $11.5\,\text{m}$ | $200\,\text{m}$ | $5\%$ Discount | $\approx \$18,500 / \text{day}$ |
| **Panamax** | $75,000\,\text{MT}$ | $13.5\,\text{m}$ | $225\,\text{m}$ | $10\%$ Discount | $\approx \$23,000 / \text{day}$ |
| **Capesize** | $170,000\,\text{MT}$ | $17.5\,\text{m}$ | $290\,\text{m}$ | $15\%$ Discount | $\approx \$36,000 / \text{day}$ |

---

## 🏆 Key Real-World Maritime Insights Discovered

1. **The Haldia Paradox:**  
   Haldia Dock Complex (HDC) on the Hooghly estuary has a strict $\le 8.5\,\text{m}$ draft limit. Sponsoring steel shipments directly via Capesize to Haldia is physically impossible. MARIVANCE automatically flags this hazard and routes to Gangavaram or Dhamra with an integrated coastal/railway rake delivery plan to Durgapur and Bokaro steel plants.
2. **Gangavaram Deepwater Arbitrage:**  
   While Paradip incurs an average queue delay of $4.8\,\text{days}$ with high laytime penalties, private deepwater Gangavaram operates at an average turnaround of $1.1\,\text{days}$ with full $18.2\,\text{m}$ draft clearance. Diverting Capesize coal shipments saves between **$70,000 and $105,000 in demurrage penalties per voyage**.
3. **Russian Far-East Hedge:**  
   Vostochny to Vizag ($\approx 4,500\,\text{NM}$) is over $500\,\text{NM}$ shorter than standard routes from Hay Point, Australia. MARIVANCE provides forward hedging recommendations during Australian coking coal price spikes.

---

## 👥 Contributors & Acknowledgements

- **Developed for:** Smart India Hackathon (SIH 2026) • Round 2 • PS 26006
- **Target Organization:** Ministry of Steel, Government of India
- **Beneficiaries:** Steel Authority of India Limited (SAIL) & Rashtriya Ispat Nigam Limited (RINL)

---
*MARIVANCE — Pioneering Autonomous Maritime Intelligence for Atmanirbhar Bharat.*
