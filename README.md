# 🔷 Simple Stock Data Pipeline

> Automated pipeline for downloading, storing, and updating historical stock market data

A Python class-based pipeline that automates the full data collection workflow for equity portfolios — from initial download to incremental updates — storing structured historical data ready for analysis, backtesting, or modeling.

---

## 📌 What It Does

1. **Data Download** — Fetches historical OHLCV data for any list of tickers via `yfinance`, storing each as a local `.csv` file
2. **Data Loading** — Loads any individual ticker's stored data into a clean `DataFrame`
3. **Incremental Update** — Detects the last stored date and downloads only the missing records, keeping data fresh without redundant calls
4. **Portfolio Consolidation** — Merges all tickers' closing prices into a single `DataFrame` — ready to feed into a risk model, optimizer, or visualization

---

## 💡 Why I Built This

Before running any portfolio analysis, you need clean, reliable data. Downloading raw data manually every time is inefficient and error-prone. This pipeline solves the data layer — so any downstream project (risk analysis, valuation, optimization) has a single, consistent data source to pull from.

---

## ⚙️ How It Works

```python
tickers = ['AAPL', 'MSFT', 'GOOGL', 'AMZN', 'TSLA']
pipeline = StockDataPipeline(tickers)

# Initial download — stores each ticker as CSV
pipeline.download_data(period='2y')

# Load a single stock
aapl = pipeline.load_data('AAPL')

# Get all closing prices in one DataFrame
portfolio = pipeline.get_portfolio_data()

# Incremental update — only fetches new records
pipeline.update_data()
```

---

## 🛠️ Tech Stack

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![yFinance](https://img.shields.io/badge/yFinance-6C63FF?style=for-the-badge&logo=yahoo&logoColor=white)

---

## 📁 Project Structure

```
📁 simple-stock-data-pipeline
├── README.md
├── requirements.txt
├── pipeline.ipynb          ← main notebook
└── /stock_data             ← auto-created folder with CSV files
    ├── AAPL.csv
    ├── MSFT.csv
    └── ...
```

---

## 🚀 How to Run

1. Clone the repository
```bash
git clone https://github.com/lbm-marangoni/stock-data-pipeline
cd stock-data-pipeline
```

2. Install dependencies
```bash
pip install -r requirements.txt
```

3. Run the notebook `pipeline.ipynb`

---

*Built by [Lucas Marangoni](https://www.linkedin.com/in/lbm-marangoni) — Economics student at FAAP | Quant Finance & Portfolio Management*