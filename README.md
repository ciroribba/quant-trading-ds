# Quant Trading Data Science

A quantitative trading research project built with Python to explore, evaluate, and validate systematic trading strategies using historical market data.

The project is developed incrementally, starting from exploratory data analysis and simple rule-based strategies before introducing more advanced statistical and machine learning techniques.

> **Current status:** V1 — Data Collection & Initial Exploration

## 🎯 Project Objective

The main objective is to investigate whether systematic trading strategies can produce measurable statistical advantages over simple benchmark strategies such as Buy & Hold.

Rather than attempting to predict market prices directly, this project focuses on:

* Financial data analysis
* Feature engineering
* Quantitative trading strategies
* Backtesting
* Risk analysis
* Statistical validation
* Reproducible research

The initial experiment uses **Bitcoin (BTC-USD)** and a simple trend-following strategy based on moving averages.

## 🔬 Initial Research Question

> Can a simple moving-average trend-following strategy outperform Buy & Hold when both return and risk are considered?

The initial strategy will evaluate two simple moving averages:

* **SMA 20** — short-term trend
* **SMA 50** — medium-term trend

The basic hypothesis is:

```text
SMA 20 > SMA 50  →  Long position
SMA 20 ≤ SMA 50  →  No position
```

This hypothesis will later be evaluated through historical backtesting and compared against a Buy & Hold benchmark.

## 📊 Dataset

The initial dataset contains historical daily market data for:

```text
BTC-USD
```

Data is retrieved programmatically using `yfinance`.

The initial period starts on:

```text
2018-01-01
```

Available market variables include:

* Open
* High
* Low
* Close
* Adjusted Close
* Volume

Raw datasets are generated locally and are intentionally excluded from version control.

## 📁 Project Structure

```text
quant-trading-ds/
│
├── data/
│   ├── raw/
│   │   └── .gitkeep
│   └── processed/
│       └── .gitkeep
│
├── notebooks/
│   ├── 01_data_collection.ipynb
│   ├── 02_eda.ipynb
│   └── 03_strategy_backtest.ipynb
│
├── src/
│   ├── data/
│   ├── features/
│   ├── strategies/
│   └── evaluation/
│
├── reports/
│   └── figures/
│
├── .gitignore
├── README.md
└── requirements.txt
```

## 📓 Notebooks

### 01 — Data Collection

`01_data_collection.ipynb`

Responsible for:

* Downloading historical BTC-USD data
* Inspecting the dataset structure
* Checking data types
* Generating descriptive statistics
* Detecting missing values
* Visualizing the historical closing price
* Saving the raw dataset locally

### 02 — Exploratory Data Analysis

`02_eda.ipynb`

Planned analysis:

* Daily returns
* Return distributions
* Volatility
* Extreme observations
* Moving averages
* Initial feature engineering

### 03 — Strategy & Backtesting

`03_strategy_backtest.ipynb`

Planned analysis:

* Trading signal generation
* Strategy returns
* Buy & Hold benchmark
* Transaction costs
* Performance metrics
* Risk metrics

## 🛠️ Technology Stack

* Python
* Pandas
* NumPy
* Matplotlib
* yfinance
* Jupyter Notebook
* Anaconda / Conda

Future versions may introduce additional statistical and machine learning tools as the research evolves.

## 🔄 Research Pipeline

```text
Market Data
    │
    ▼
Data Collection
    │
    ▼
Exploratory Data Analysis
    │
    ▼
Feature Engineering
    │
    ▼
Trading Signals
    │
    ▼
Backtesting
    │
    ├──── Buy & Hold Benchmark
    │
    ▼
Risk & Performance Analysis
    │
    ▼
Temporal Validation
```

## 📈 Planned Metrics

Strategies will eventually be evaluated using metrics including:

* Cumulative Return
* Annualized Return
* Volatility
* Sharpe Ratio
* Maximum Drawdown
* Win Rate
* Profit Factor
* Number of Trades

## 📚 Glosario

El proyecto incluye un glosario con los principales conceptos
financieros, estadísticos y de Data Science utilizados durante
el desarrollo.

Ver: [`docs/glossary.md`](docs/glossary.md)

## ⚠️ Disclaimer

This project is intended for educational, research, and portfolio purposes only.

It does not constitute financial advice, investment advice, or a recommendation to buy or sell any financial asset.

Past performance does not guarantee future results.

## 🚧 Project Status

### V1 — Quantitative Trend Strategy

* [x] Project structure
* [x] Data collection
* [x] Initial data inspection
* [x] Closing price visualization
* [x] Exploratory data analysis
* [x] Return analysis
* [x] Initial feature engineering
* [ ] Trading signal generation
* [ ] Backtesting
* [ ] Benchmark comparison
* [ ] Risk analysis
* [ ] Temporal validation
* [ ] Final V1 report

---

**Status:** Work in progress 🚧
