# Simple Stock Data Pipeline

A lightweight Python pipeline for collecting, storing, updating and consolidating historical equity market data for investment analysis and portfolio research.

The project focuses on the **data layer** of an investment workflow: keeping market data organized and reusable so downstream analyses can work from a consistent local source.

---

## Why I Built It

Before performing portfolio analysis, risk calculations or quantitative research, the underlying data needs to be accessible and consistently structured.

Repeatedly downloading the same historical data manually is inefficient and makes research workflows harder to reproduce.

This project was built to automate that basic infrastructure.

> The objective is not to analyze investments directly, but to create a reliable input layer for other investment-research tools.

---

## Data Workflow

```text
Ticker Universe
      ↓
Market Data Download
      ↓
Local Storage
      ↓
Incremental Updates
      ↓
Data Consolidation
      ↓
Investment / Portfolio Analysis
```

The pipeline separates data collection from downstream analysis so the same stored dataset can be reused across different projects.

---

## What It Does

### 1. Initial Data Collection

Downloads historical OHLCV market data for a list of equities through `yfinance`.

Each ticker is stored locally as an individual CSV file.

### 2. Local Data Loading

Loads previously stored data into Pandas DataFrames for analysis.

### 3. Incremental Updates

Checks the most recent stored observation and requests only newer market data.

This avoids rebuilding the entire dataset whenever the pipeline is updated.

### 4. Portfolio Data Consolidation

Combines closing-price series from multiple equities into a single DataFrame.

The resulting dataset can be used as an input for:

- return calculations
- correlation analysis
- portfolio risk analysis
- visualization
- backtesting experiments
- other research workflows

---

## Example

```python
tickers = ["AAPL", "MSFT", "GOOGL", "AMZN", "TSLA"]

pipeline = StockDataPipeline(tickers)

# Initial download
pipeline.download_data(period="2y")

# Load one stock
aapl = pipeline.load_data("AAPL")

# Consolidate portfolio closing prices
portfolio = pipeline.get_portfolio_data()

# Update only missing observations
pipeline.update_data()
```

---

## Technology

- Python
- Pandas
- yFinance
- Jupyter Notebook
- CSV-based local storage

The project is intentionally lightweight and focuses on workflow reliability rather than infrastructure complexity.

---

## Project Structure

```text
simple-stock-data-pipeline/
├── README.md
├── requirements.txt
├── pipeline.ipynb
└── stock_data/
    ├── AAPL.csv
    ├── MSFT.csv
    └── ...
```

The `stock_data/` directory is created automatically when the pipeline runs.

---

## Running the Project

Clone the repository:

```bash
git clone https://github.com/lbm-marangoni/simple-stock-data-pipeline
cd simple-stock-data-pipeline
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Then run:

```text
pipeline.ipynb
```

---

## Limitations

The current version is intentionally simple.

Its main limitations include:

- reliance on `yfinance` as the market-data source
- CSV-based storage rather than a database
- limited data validation
- no corporate-action normalization layer beyond what the source provides
- no automated testing
- no production-grade data orchestration

These constraints are appropriate for the project's purpose as a small research utility rather than a production market-data platform.

---

## Role in My Investment Process

This repository represents the **data infrastructure layer** behind investment and portfolio analysis.

Its role is complementary to projects focused on research and decision-making.

For broader investment-process work, see:

**[SBWAA — Investment Research & Portfolio Decision-Support System](https://github.com/lbm-marangoni/sbwaa)**

For an example of a first-stage company filtering tool, see:

**[Equity Screening Utility](https://github.com/lbm-marangoni/stock-screener)**

---

## Author

**Lucas Marangoni**

Economics @ FAAP  
Performance & Insights @ Bradesco  
Research @ FAAP Finance

Asset Management • Equity Research • Investment Analysis

[LinkedIn](https://www.linkedin.com/in/lbm-marangoni)

---

## Disclaimer

This repository is an educational and research project.

Market data may contain errors, omissions or inconsistencies and should be independently verified before being used for investment decisions.
