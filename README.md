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
