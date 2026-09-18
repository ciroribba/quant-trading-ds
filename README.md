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

## Project Structure

```text
quant-trading-ds/
├── data/
│   ├── raw/
│   │   └── btc_usd.csv
│   └── processed/
├── notebooks/
│   ├── 01_data_collection.ipynb
│   ├── 02_eda.ipynb
│   └── 03_strategy_backtest.ipynb
├── src/
│   ├── data/
│   ├── features/
│   ├── strategies/
│   └── evaluation/
├── docs/
│   └── glossary.md
├── reports/
│   └── figures/
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

## Methodology

The first version of the project evaluates a simple trend-following strategy
based on two Simple Moving Averages (SMA):

- **SMA 20:** short-term trend.
- **SMA 50:** medium-term trend.

The trading rule is:

- **Long (1):** SMA 20 > SMA 50
- **Out of market (0):** SMA 20 <= SMA 50

No short positions or leverage are used.

To avoid look-ahead bias, the trading position is shifted by one period so
that a signal generated using information from day `t` is applied to the
following trading period.

The strategy is evaluated against **Buy & Hold** using:

- cumulative return;
- annualized volatility;
- Sharpe Ratio;
- Maximum Drawdown;
- number of transactions;
- transaction costs.

A hypothetical transaction cost of **0.10% per transaction** is included in
the net strategy results.

## Initial Backtest Results

The historical backtest currently covers BTC-USD data from 2018 onward.

| Metric | SMA 20/50 | SMA 20/50 + Costs | Buy & Hold |
|---|---:|---:|---:|
| Cumulative Return | 642.88% | 591.93% | 582.99% |
| Annualized Volatility | 43.04% | 43.04% | 61.68% |
| Sharpe Ratio | 0.76 | 0.74 | 0.67 |
| Maximum Drawdown | -57.88% | -58.61% | -76.63% |

The strategy generated **71 transactions** during the analyzed period:

- 36 entries;
- 35 exits.

Transaction costs reduce the difference in cumulative return between the
SMA strategy and Buy & Hold considerably.

However, the historical risk profiles remain different. Under the assumptions
used in this backtest, the SMA strategy shows lower annualized volatility and
a less severe Maximum Drawdown than Buy & Hold.

These results are historical backtest results and should not be interpreted
as evidence that the strategy will produce similar results on future data.
Temporal out-of-sample validation has not yet been performed.


```
### 📚 Documentation

The [`docs/glossary.md`](docs/glossary.md) file contains definitions of the
main financial, statistical, and quantitative trading concepts used throughout
the project.

The glossary is progressively updated as new concepts are introduced during
the research and development of the strategy.
```

## ⚠️ Disclaimer

This project is intended for educational, research, and portfolio purposes only.

It does not constitute financial advice, investment advice, or a recommendation to buy or sell any financial asset.

Past performance does not guarantee future results.

## 🚧 Project Status

### V1 — Quantitative Trend Strategy

- [x] Historical BTC data collection
- [x] Data cleaning and preparation
- [x] Exploratory Data Analysis (EDA)
- [x] Daily return analysis
- [x] SMA 20 / SMA 50 feature engineering
- [x] Trading signal generation
- [x] Look-ahead bias prevention
- [x] Strategy backtesting
- [x] Buy & Hold benchmark
- [x] Risk and performance metrics
- [x] Transaction cost analysis
- [ ] Temporal train / validation / test split
- [ ] Out-of-sample evaluation
- [ ] Strategy robustness analysis
- [ ] Final V1 report

---

**Status:** Work in progress 🚧
