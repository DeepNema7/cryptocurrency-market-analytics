# 📊 Cryptocurrency Market Analytics

> End-to-end data analysis pipeline — real-time market snapshots, correlation studies, and Bitcoin price trends using public REST APIs.

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat-square&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=flat-square&logo=jupyter&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-2.x-150458?style=flat-square&logo=pandas&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-3.x-11557C?style=flat-square)
![Seaborn](https://img.shields.io/badge/Seaborn-0.13+-4C72B0?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-22C55E?style=flat-square)
![API](https://img.shields.io/badge/API-CoinGecko-8DC63F?style=flat-square&logo=coingecko&logoColor=white)

---

## Table of Contents

1. [Project Overview](#-project-overview)
2. [Objectives](#-objectives)
3. [Tech Stack](#-tech-stack)
4. [Data Sources](#-data-sources)
5. [Project Structure](#-project-structure)
6. [Analysis & Visualizations](#-analysis--visualizations)
7. [Key Insights](#-key-insights)
8. [Quickstart](#-quickstart)
9. [Requirements](#-requirements)

---

## 🧭 Project Overview

**Cryptocurrency Market Analytics** is an end-to-end data analysis project that leverages real-time cryptocurrency data from the CoinGecko public API to analyze, visualize, and interpret market behavior.

The project covers:
- Live market snapshots (price, volume, market cap)
- Short-term price movement tracking
- Correlation analysis across financial indicators
- Time-series analysis of Bitcoin prices over 30 days

---

## 🎯 Objectives

<details>
<summary><strong>1. Live API Integration</strong></summary>

Fetch real-time data via CoinGecko REST endpoints.

</details>

<details>
<summary><strong>2. Metric Analysis</strong></summary>

Analyze price, volume, and market cap across top assets.

</details>

<details>
<summary><strong>3. Correlation Study</strong></summary>

Heatmap analysis across key financial indicators.

</details>

<details>
<summary><strong>4. Time-Series Trend</strong></summary>

30-day Bitcoin price movement visualization.

</details>

## 🛠️ Tech Stack

| Tool | Version | Role |
|------|---------|------|
| **Python** | 3.10+ | Core language |
| **Jupyter Notebook** | 7.x | Interactive execution environment |
| **Pandas** | 2.x | Data manipulation & DataFrame operations |
| **Matplotlib** | 3.x | Bar charts, line plots, scatter plots |
| **Seaborn** | 0.13+ | Statistical visualizations, correlation heatmap |
| **Requests** | 2.x | HTTP client for REST API calls |

---

## 📡 Data Sources

### CoinGecko Public REST API

**Endpoint 1 — Market Snapshot**
```
GET https://api.coingecko.com/api/v3/coins/markets
```
| Parameter | Value |
|-----------|-------|
| `vs_currency` | `usd` |
| `order` | `market_cap_desc` |
| `per_page` | `10` |
| `price_change_percentage` | `24h` |

Returns: `current_price`, `market_cap`, `total_volume`, `price_change_percentage_24h`

---

**Endpoint 2 — Historical Time-Series**
```
GET https://api.coingecko.com/api/v3/coins/bitcoin/market_chart
```
| Parameter | Value |
|-----------|-------|
| `vs_currency` | `usd` |
| `days` | `30` |

Returns: Historical Bitcoin prices over the last 30 days.

---

## 📁 Project Structure

```
cryptocurrency-market-analytics/
│
├── crypto_market_analysis.ipynb   # Main analysis notebook
├── requirements.txt               # Python dependencies
├── README.md                      # Project documentation
│
└── assets/                        # Generated visualizations
    ├── current_price.png
    ├── trading_volume_24h.png
    ├── volume_vs_price.png
    ├── crypto_market_correlation.png
    └── bitcoin_price_trend_30_days.png
```

---

## 📈 Analysis & Visualizations

### 1. Market Snapshot Analysis
Compares current price, market cap, and 24h trading volume across the top 10 cryptocurrencies using bar charts.

```python
import requests
import pandas as pd

url = "https://api.coingecko.com/api/v3/coins/markets"
params = {
    "vs_currency": "usd",
    "order": "market_cap_desc",
    "per_page": 10,
    "price_change_percentage": "24h"
}

response = requests.get(url, params=params)
df = pd.DataFrame(response.json())
print(df[["name", "current_price", "market_cap", "total_volume"]])
```

---

### 2. Volume vs Price Scatter Plot
Maps 24h trading volume against spot price to reveal liquidity and dominance patterns.

```python
import matplotlib.pyplot as plt

plt.figure(figsize=(10, 6))
plt.scatter(df["total_volume"], df["current_price"], color="steelblue", alpha=0.7, s=80)

for i, row in df.iterrows():
    plt.annotate(row["symbol"].upper(), (row["total_volume"], row["current_price"]),
                 fontsize=8, ha="right")

plt.xlabel("24h Trading Volume (USD)")
plt.ylabel("Current Price (USD)")
plt.title("Volume vs Price — Top 10 Cryptocurrencies")
plt.tight_layout()
plt.savefig("assets/volume_vs_price.png", dpi=150)
plt.show()
```

---

### 3. Correlation Heatmap
Computes Pearson correlation coefficients across price, volume, market cap, and 24h change.

```python
import seaborn as sns

cols = ["current_price", "market_cap", "total_volume", "price_change_percentage_24h"]
corr = df[cols].corr()

plt.figure(figsize=(8, 6))
sns.heatmap(corr, annot=True, fmt=".2f", cmap="coolwarm",
            linewidths=0.5, square=True, cbar_kws={"shrink": 0.8})

plt.title("Correlation Heatmap — Market Indicators")
plt.tight_layout()
plt.savefig("assets/crypto_market_correlation.png", dpi=150)
plt.show()
```

---

### 4. Bitcoin 30-Day Time-Series
Fetches historical BTC prices and plots date-wise trend with moving average.

```python
import matplotlib.dates as mdates
from datetime import datetime

url = "https://api.coingecko.com/api/v3/coins/bitcoin/market_chart"
params = {"vs_currency": "usd", "days": 30}

data = requests.get(url, params=params).json()
prices = data["prices"]

btc_df = pd.DataFrame(prices, columns=["timestamp", "price"])
btc_df["date"] = pd.to_datetime(btc_df["timestamp"], unit="ms")

plt.figure(figsize=(12, 5))
plt.plot(btc_df["date"], btc_df["price"], color="#F0883E", linewidth=1.8, label="BTC Price")
plt.fill_between(btc_df["date"], btc_df["price"], alpha=0.1, color="#F0883E")

plt.gca().xaxis.set_major_formatter(mdates.DateFormatter("%b %d"))
plt.gca().xaxis.set_major_locator(mdates.WeekdayLocator())
plt.xticks(rotation=45)

plt.xlabel("Date")
plt.ylabel("Price (USD)")
plt.title("Bitcoin Price Trend — Last 30 Days")
plt.legend()
plt.tight_layout()
plt.savefig("assets/bitcoin_price_trend_30_days.png", dpi=150)
plt.show()
```

---

## 🧠 Key Insights

> **Correlation** — Market capitalization shows strong positive correlation with trading volume across all major assets.

> **Volatility** — High-volume assets exhibit greater price stability relative to low-liquidity micro-caps.

> **Trend** — Bitcoin displays short-term volatility clusters but maintains clear directional trend behavior over 30-day windows.

> **API Design** — Snapshot vs time-series endpoints serve fundamentally different analytical purposes; market snapshots capture state, time-series captures motion.

---

## 🚀 Quickstart

**1. Clone the repository**
```bash
git clone https://github.com/your-username/cryptocurrency-market-analytics.git
cd cryptocurrency-market-analytics
```

**2. Create a virtual environment**
```bash
python -m venv .venv

# macOS / Linux
source .venv/bin/activate

# Windows
.venv\Scripts\activate
```

**3. Install dependencies**
```bash
pip install -r requirements.txt
```

**4. Launch Jupyter Notebook**
```bash
jupyter notebook crypto_market_analysis.ipynb
```

**5. Run all cells**

`Kernel` → `Restart & Run All`

---

## 📦 Requirements

`requirements.txt`
```
requests>=2.31.0
pandas>=2.0.0
matplotlib>=3.7.0
seaborn>=0.13.0
jupyter>=1.0.0
notebook>=7.0.0
```

Install directly:
```bash
pip install requests pandas matplotlib seaborn jupyter notebook
```

---


<div align="center">
  <sub>Built with Python · Data from CoinGecko Public API · No API key required</sub>
</div>
