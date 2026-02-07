Project Overview

Cryptocurrency Market Analytics is an end-to-end data analysis project that leverages real-time cryptocurrency data from public APIs to analyze, visualize, and interpret market behavior.

The project focuses on:

Market snapshots (price, volume, market cap)

Short-term price movement

Correlation between financial indicators

Time-series analysis of Bitcoin prices

🎯 Objectives

Fetch live cryptocurrency market data using REST APIs

Analyze key financial metrics (price, volume, market cap)

Perform correlation analysis across market indicators

Build clean, insightful visualizations

Conduct time-series analysis on Bitcoin price trends

🛠️ Tech Stack & Tools

Python

Jupyter Notebook

Pandas – data manipulation & analysis

Matplotlib – data visualization

Seaborn – statistical visualizations

Requests – REST API integration

📡 Data Source

CoinGecko Public REST API

/coins/markets → market snapshot data

/coins/{id}/market_chart → historical time-series data

Metrics Used:

Current Price (USD)

Market Capitalization

Trading Volume (24h)

Price Change Percentage (24h)

Historical Bitcoin Prices (30 Days)

📈 Key Analysis & Visualizations

🔹 Market Snapshot Analysis

Current price comparison across top cryptocurrencies

Market capitalization comparison

24-hour trading volume analysis

24-hour price change percentage

🔹 Relationship Analysis

Volume vs Price scatter analysis

Correlation heatmap of key financial indicators

🔹 Time-Series Analysis

Bitcoin price trend over the last 30 days

Date-wise price movement visualization

images/

├── current_price.png

├── market_cap.png

├── trading_volume_24h.png

├── price_change_24h.png

├── volume_vs_price.png

├── crypto_market_correlation.png

└── bitcoin_price_last_30_days.png
