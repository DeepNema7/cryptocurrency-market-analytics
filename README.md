<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Crypto Market Analytics — README</title>
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@400;500;600&family=IBM+Plex+Sans:wght@300;400;500;600&display=swap" rel="stylesheet"/>
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --bg:        #0d1117;
    --bg2:       #161b22;
    --bg3:       #1c2128;
    --border:    #30363d;
    --border2:   #21262d;
    --text:      #e6edf3;
    --muted:     #7d8590;
    --accent:    #f0883e;
    --accent2:   #58a6ff;
    --green:     #3fb950;
    --red:       #f85149;
    --mono:      'IBM Plex Mono', monospace;
    --sans:      'IBM Plex Sans', sans-serif;
  }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: var(--sans);
    font-size: 15px;
    line-height: 1.7;
    min-height: 100vh;
  }

  a { color: var(--accent2); text-decoration: none; }
  a:hover { text-decoration: underline; }

  /* ── Layout ── */
  .page { max-width: 860px; margin: 0 auto; padding: 0 24px 80px; }

  /* ── Top bar ── */
  .topbar {
    border-bottom: 1px solid var(--border);
    padding: 14px 0;
    display: flex;
    align-items: center;
    gap: 10px;
    margin-bottom: 0;
  }

  .topbar-path {
    font-family: var(--mono);
    font-size: 13px;
    color: var(--muted);
  }

  .topbar-path span { color: var(--accent2); }

  .badge-row {
    margin-left: auto;
    display: flex;
    gap: 6px;
  }

  .badge {
    font-family: var(--mono);
    font-size: 11px;
    padding: 2px 10px;
    border-radius: 2em;
    border: 1px solid;
    white-space: nowrap;
  }

  .badge-python  { color: #79c0ff; border-color: #1f4a7a; background: #0d2748; }
  .badge-jupyter { color: #f0883e; border-color: #7a3d10; background: #2e1800; }
  .badge-license { color: #3fb950; border-color: #1a4a24; background: #0d2a12; }

  /* ── Hero ── */
  .hero {
    padding: 48px 0 36px;
    border-bottom: 1px solid var(--border);
  }

  .hero-eyebrow {
    font-family: var(--mono);
    font-size: 12px;
    color: var(--muted);
    letter-spacing: 0.08em;
    margin-bottom: 14px;
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .live-dot {
    width: 7px; height: 7px;
    border-radius: 50%;
    background: var(--green);
    box-shadow: 0 0 0 0 rgba(63,185,80,0.5);
    animation: ping 2.2s ease infinite;
  }

  @keyframes ping {
    0%   { box-shadow: 0 0 0 0 rgba(63,185,80,0.45); }
    70%  { box-shadow: 0 0 0 7px rgba(63,185,80,0); }
    100% { box-shadow: 0 0 0 0 rgba(63,185,80,0); }
  }

  .hero h1 {
    font-family: var(--sans);
    font-size: clamp(1.75rem, 4vw, 2.6rem);
    font-weight: 600;
    letter-spacing: -0.02em;
    line-height: 1.2;
    color: var(--text);
  }

  .hero h1 em {
    font-style: normal;
    color: var(--accent);
  }

  .hero-desc {
    margin-top: 14px;
    font-size: 15px;
    font-weight: 300;
    color: var(--muted);
    max-width: 560px;
    line-height: 1.75;
  }

  .hero-stats {
    display: flex;
    gap: 32px;
    margin-top: 28px;
    flex-wrap: wrap;
  }

  .stat-item { display: flex; flex-direction: column; gap: 2px; }

  .stat-num {
    font-family: var(--mono);
    font-size: 20px;
    font-weight: 600;
    color: var(--text);
  }

  .stat-num.green { color: var(--green); }
  .stat-num.orange { color: var(--accent); }

  .stat-label {
    font-family: var(--mono);
    font-size: 11px;
    color: var(--muted);
    letter-spacing: 0.06em;
  }

  /* ── TOC ── */
  .toc {
    margin: 32px 0;
    background: var(--bg2);
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 20px 24px;
  }

  .toc-title {
    font-family: var(--mono);
    font-size: 11px;
    color: var(--muted);
    letter-spacing: 0.1em;
    margin-bottom: 12px;
    text-transform: uppercase;
  }

  .toc ol {
    list-style: none;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 4px 24px;
    counter-reset: toc;
  }

  .toc li { counter-increment: toc; }

  .toc a {
    font-size: 13.5px;
    color: var(--muted);
    display: flex;
    align-items: center;
    gap: 8px;
    padding: 3px 0;
    transition: color 0.15s;
  }

  .toc a::before {
    content: counter(toc, decimal-leading-zero);
    font-family: var(--mono);
    font-size: 10px;
    color: var(--border);
  }

  .toc a:hover { color: var(--accent2); text-decoration: none; }

  /* ── Sections ── */
  .section { margin-top: 48px; }

  .section-header {
    display: flex;
    align-items: center;
    gap: 12px;
    margin-bottom: 20px;
    padding-bottom: 12px;
    border-bottom: 1px solid var(--border);
  }

  .section-num {
    font-family: var(--mono);
    font-size: 11px;
    color: var(--muted);
    min-width: 28px;
  }

  .section-title {
    font-size: 18px;
    font-weight: 600;
    letter-spacing: -0.01em;
    color: var(--text);
  }

  /* ── Objective cards ── */
  .obj-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(190px, 1fr));
    gap: 12px;
  }

  .obj-card {
    background: var(--bg2);
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 18px;
    transition: border-color 0.2s, background 0.2s;
  }

  .obj-card:hover {
    border-color: var(--accent2);
    background: var(--bg3);
  }

  .obj-card-icon {
    font-size: 18px;
    margin-bottom: 10px;
    line-height: 1;
  }

  .obj-card-title {
    font-size: 13.5px;
    font-weight: 600;
    color: var(--text);
    margin-bottom: 4px;
  }

  .obj-card-desc {
    font-size: 12.5px;
    color: var(--muted);
    line-height: 1.55;
  }

  /* ── Stack ── */
  .stack-table {
    width: 100%;
    border-collapse: collapse;
    font-size: 13.5px;
  }

  .stack-table th {
    font-family: var(--mono);
    font-size: 11px;
    color: var(--muted);
    text-align: left;
    padding: 0 12px 10px;
    letter-spacing: 0.06em;
    border-bottom: 1px solid var(--border);
  }

  .stack-table th:first-child { padding-left: 0; }

  .stack-table td {
    padding: 11px 12px;
    border-bottom: 1px solid var(--border2);
    vertical-align: top;
  }

  .stack-table td:first-child { padding-left: 0; }
  .stack-table tr:last-child td { border-bottom: none; }

  .stack-table tr:hover td { background: var(--bg2); }

  .tool-name {
    font-family: var(--mono);
    font-size: 13px;
    font-weight: 500;
    color: var(--accent2);
  }

  .tool-ver {
    font-family: var(--mono);
    font-size: 11px;
    color: var(--muted);
    margin-top: 2px;
  }

  .tool-role { color: var(--muted); font-size: 13px; }

  /* ── API block ── */
  .api-block {
    border: 1px solid var(--border);
    border-radius: 6px;
    overflow: hidden;
    margin-bottom: 16px;
  }

  .api-head {
    background: var(--bg2);
    padding: 12px 16px;
    display: flex;
    align-items: center;
    gap: 12px;
    border-bottom: 1px solid var(--border);
  }

  .method-badge {
    font-family: var(--mono);
    font-size: 10px;
    font-weight: 600;
    padding: 2px 8px;
    border-radius: 3px;
    background: #1a3a1a;
    color: var(--green);
    letter-spacing: 0.05em;
  }

  .endpoint {
    font-family: var(--mono);
    font-size: 13px;
    color: var(--text);
  }

  .endpoint-desc {
    margin-left: auto;
    font-size: 12px;
    color: var(--muted);
  }

  .api-body {
    padding: 14px 16px;
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
  }

  .param-tag {
    font-family: var(--mono);
    font-size: 11.5px;
    padding: 4px 10px;
    border-radius: 3px;
    background: var(--bg3);
    border: 1px solid var(--border);
    color: var(--muted);
  }

  /* ── Analysis list ── */
  .analysis-table {
    width: 100%;
    border-collapse: collapse;
    font-size: 13.5px;
  }

  .analysis-table tr {
    border-bottom: 1px solid var(--border2);
    transition: background 0.15s;
  }

  .analysis-table tr:last-child { border-bottom: none; }
  .analysis-table tr:hover { background: var(--bg2); }

  .analysis-table td {
    padding: 14px 12px;
    vertical-align: top;
  }

  .analysis-table td:first-child { padding-left: 0; width: 32px; }
  .analysis-table td:last-child { padding-right: 0; }

  .a-num {
    font-family: var(--mono);
    font-size: 11px;
    color: var(--accent);
    padding-top: 2px;
  }

  .a-title {
    font-weight: 500;
    color: var(--text);
    font-size: 14px;
    margin-bottom: 3px;
  }

  .a-desc { color: var(--muted); font-size: 13px; line-height: 1.5; }

  .a-tags { display: flex; gap: 6px; flex-wrap: wrap; margin-top: 8px; }

  .a-tag {
    font-family: var(--mono);
    font-size: 10.5px;
    padding: 2px 8px;
    border-radius: 2px;
    background: var(--bg3);
    border: 1px solid var(--border);
    color: var(--muted);
  }

  /* ── Insights ── */
  .insights-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
    gap: 12px;
  }

  .insight-card {
    background: var(--bg2);
    border: 1px solid var(--border);
    border-left: 3px solid;
    border-radius: 0 6px 6px 0;
    padding: 16px 18px;
  }

  .insight-card.c1 { border-left-color: var(--accent2); }
  .insight-card.c2 { border-left-color: var(--accent); }
  .insight-card.c3 { border-left-color: var(--green); }

  .insight-label {
    font-family: var(--mono);
    font-size: 10px;
    letter-spacing: 0.1em;
    color: var(--muted);
    margin-bottom: 8px;
  }

  .insight-text {
    font-size: 13.5px;
    color: var(--text);
    line-height: 1.6;
    font-weight: 300;
  }

  /* ── Quickstart ── */
  .code-block {
    background: var(--bg2);
    border: 1px solid var(--border);
    border-radius: 6px;
    overflow: hidden;
    margin-top: 12px;
  }

  .code-head {
    background: var(--bg3);
    padding: 8px 16px;
    border-bottom: 1px solid var(--border);
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .code-lang {
    font-family: var(--mono);
    font-size: 11px;
    color: var(--muted);
    letter-spacing: 0.06em;
  }

  .code-copy {
    font-family: var(--mono);
    font-size: 10px;
    color: var(--muted);
    background: none;
    border: 1px solid var(--border);
    border-radius: 3px;
    padding: 2px 8px;
    cursor: pointer;
    transition: color 0.15s, border-color 0.15s;
  }

  .code-copy:hover { color: var(--accent2); border-color: var(--accent2); }

  pre {
    font-family: var(--mono);
    font-size: 13px;
    line-height: 1.7;
    padding: 18px 20px;
    overflow-x: auto;
    color: var(--text);
  }

  .c-comment { color: #6e7681; }
  .c-cmd     { color: var(--green); }
  .c-str     { color: #a5d6ff; }
  .c-kw      { color: #ff7b72; }
  .c-fn      { color: #d2a8ff; }

  /* ── Footer ── */
  .footer {
    margin-top: 60px;
    padding-top: 24px;
    border-top: 1px solid var(--border);
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-wrap: wrap;
    gap: 12px;
  }

  .footer-left {
    font-family: var(--mono);
    font-size: 12px;
    color: var(--muted);
  }

  .footer-right {
    display: flex;
    gap: 20px;
  }

  .footer-link {
    font-family: var(--mono);
    font-size: 12px;
    color: var(--muted);
    transition: color 0.15s;
  }

  .footer-link:hover { color: var(--accent2); text-decoration: none; }

  /* ── Divider ── */
  hr { border: none; border-top: 1px solid var(--border); margin: 0; }

  /* ── Scrollbar ── */
  ::-webkit-scrollbar { width: 6px; height: 6px; }
  ::-webkit-scrollbar-track { background: var(--bg); }
  ::-webkit-scrollbar-thumb { background: var(--border); border-radius: 3px; }
</style>
</head>
<body>

<div class="page">

  <!-- Top bar -->
  <div class="topbar">
    <span class="topbar-path">
      <span>crypto-market-analytics</span> / README.md
    </span>
    <div class="badge-row">
      <span class="badge badge-python">Python 3.10+</span>
      <span class="badge badge-jupyter">Jupyter</span>
      <span class="badge badge-license">MIT</span>
    </div>
  </div>

  <!-- Hero -->
  <div class="hero">
    <div class="hero-eyebrow">
      <div class="live-dot"></div>
      COINGECKO API &nbsp;·&nbsp; END-TO-END ANALYTICS &nbsp;·&nbsp; DATA SCIENCE
    </div>
    <h1>Cryptocurrency<br/><em>Market Analytics</em></h1>
    <p class="hero-desc">
      A data analysis pipeline that fetches live cryptocurrency market data,
      performs correlation studies across financial indicators, and visualizes
      Bitcoin price trends over a 30-day window.
    </p>
    <div class="hero-stats">
      <div class="stat-item">
        <span class="stat-num">5</span>
        <span class="stat-label">METRICS TRACKED</span>
      </div>
      <div class="stat-item">
        <span class="stat-num orange">4</span>
        <span class="stat-label">VISUALIZATIONS</span>
      </div>
      <div class="stat-item">
        <span class="stat-num green">30d</span>
        <span class="stat-label">BTC TIME SERIES</span>
      </div>
      <div class="stat-item">
        <span class="stat-num">2</span>
        <span class="stat-label">API ENDPOINTS</span>
      </div>
    </div>
  </div>

  <!-- TOC -->
  <div class="toc">
    <div class="toc-title">Table of Contents</div>
    <ol>
      <li><a href="#objectives">Objectives</a></li>
      <li><a href="#tech-stack">Tech Stack</a></li>
      <li><a href="#data-sources">Data Sources</a></li>
      <li><a href="#analysis">Analysis &amp; Visualizations</a></li>
      <li><a href="#insights">Key Insights</a></li>
      <li><a href="#quickstart">Quickstart</a></li>
    </ol>
  </div>

  <!-- Objectives -->
  <div class="section" id="objectives">
    <div class="section-header">
      <span class="section-num">01</span>
      <span class="section-title">Objectives</span>
    </div>
    <div class="obj-grid">
      <div class="obj-card">
        <div class="obj-card-icon">📡</div>
        <div class="obj-card-title">Live API Integration</div>
        <div class="obj-card-desc">Fetch real-time market data through CoinGecko's public REST endpoints.</div>
      </div>
      <div class="obj-card">
        <div class="obj-card-icon">📊</div>
        <div class="obj-card-title">Metric Analysis</div>
        <div class="obj-card-desc">Analyze price, volume, and market cap across top-ranked cryptocurrencies.</div>
      </div>
      <div class="obj-card">
        <div class="obj-card-icon">🔗</div>
        <div class="obj-card-title">Correlation Study</div>
        <div class="obj-card-desc">Heatmap analysis revealing relationships between key financial indicators.</div>
      </div>
      <div class="obj-card">
        <div class="obj-card-icon">📈</div>
        <div class="obj-card-title">Time-Series Trend</div>
        <div class="obj-card-desc">30-day Bitcoin price movement with date-wise visualization.</div>
      </div>
    </div>
  </div>

  <!-- Tech Stack -->
  <div class="section" id="tech-stack">
    <div class="section-header">
      <span class="section-num">02</span>
      <span class="section-title">Tech Stack</span>
    </div>
    <table class="stack-table">
      <thead>
        <tr>
          <th>TOOL</th>
          <th>VERSION</th>
          <th>ROLE</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td><div class="tool-name">Python</div></td>
          <td><div class="tool-ver">3.10+</div></td>
          <td><div class="tool-role">Core language for all scripts and analysis</div></td>
        </tr>
        <tr>
          <td><div class="tool-name">Jupyter Notebook</div></td>
          <td><div class="tool-ver">7.x</div></td>
          <td><div class="tool-role">Interactive execution environment</div></td>
        </tr>
        <tr>
          <td><div class="tool-name">Pandas</div></td>
          <td><div class="tool-ver">2.x</div></td>
          <td><div class="tool-role">Data manipulation, DataFrame operations, aggregations</div></td>
        </tr>
        <tr>
          <td><div class="tool-name">Matplotlib</div></td>
          <td><div class="tool-ver">3.x</div></td>
          <td><div class="tool-role">Base charting: bar charts, line plots, scatter plots</div></td>
        </tr>
        <tr>
          <td><div class="tool-name">Seaborn</div></td>
          <td><div class="tool-ver">0.13+</div></td>
          <td><div class="tool-role">Statistical visualizations, correlation heatmap</div></td>
        </tr>
        <tr>
          <td><div class="tool-name">Requests</div></td>
          <td><div class="tool-ver">2.x</div></td>
          <td><div class="tool-role">HTTP client for CoinGecko REST API calls</div></td>
        </tr>
      </tbody>
    </table>
  </div>

  <!-- Data Sources -->
  <div class="section" id="data-sources">
    <div class="section-header">
      <span class="section-num">03</span>
      <span class="section-title">Data Sources</span>
    </div>

    <div class="api-block">
      <div class="api-head">
        <span class="method-badge">GET</span>
        <span class="endpoint">/coins/markets</span>
        <span class="endpoint-desc">Market snapshot data</span>
      </div>
      <div class="api-body">
        <span class="param-tag">current_price (USD)</span>
        <span class="param-tag">market_cap</span>
        <span class="param-tag">total_volume</span>
        <span class="param-tag">price_change_percentage_24h</span>
      </div>
    </div>

    <div class="api-block">
      <div class="api-head">
        <span class="method-badge">GET</span>
        <span class="endpoint">/coins/{id}/market_chart</span>
        <span class="endpoint-desc">Historical time-series</span>
      </div>
      <div class="api-body">
        <span class="param-tag">bitcoin historical prices</span>
        <span class="param-tag">days=30</span>
        <span class="param-tag">vs_currency=usd</span>
      </div>
    </div>
  </div>

  <!-- Analysis -->
  <div class="section" id="analysis">
    <div class="section-header">
      <span class="section-num">04</span>
      <span class="section-title">Analysis &amp; Visualizations</span>
    </div>

    <table class="analysis-table">
      <tbody>
        <tr>
          <td><div class="a-num">01</div></td>
          <td>
            <div class="a-title">Market Snapshot Analysis</div>
            <div class="a-desc">Current price comparison, market capitalization ranking, 24h trading volume, and price change percentage across top cryptocurrencies.</div>
            <div class="a-tags">
              <span class="a-tag">bar chart</span>
              <span class="a-tag">matplotlib</span>
              <span class="a-tag">/coins/markets</span>
            </div>
          </td>
        </tr>
        <tr>
          <td><div class="a-num">02</div></td>
          <td>
            <div class="a-title">Volume vs Price Scatter</div>
            <div class="a-desc">Scatter plot mapping 24h trading volume against current price to reveal liquidity and market dominance patterns.</div>
            <div class="a-tags">
              <span class="a-tag">scatter plot</span>
              <span class="a-tag">matplotlib</span>
              <span class="a-tag">relationship analysis</span>
            </div>
          </td>
        </tr>
        <tr>
          <td><div class="a-num">03</div></td>
          <td>
            <div class="a-title">Correlation Heatmap</div>
            <div class="a-desc">Seaborn heatmap computing Pearson correlation coefficients across price, volume, market cap, and 24h change indicators.</div>
            <div class="a-tags">
              <span class="a-tag">heatmap</span>
              <span class="a-tag">seaborn</span>
              <span class="a-tag">pearson correlation</span>
            </div>
          </td>
        </tr>
        <tr>
          <td><div class="a-num">04</div></td>
          <td>
            <div class="a-title">Bitcoin 30-Day Time-Series</div>
            <div class="a-desc">Line chart of Bitcoin's historical price from the market_chart API — exposes trend direction, resistance zones, and short-term volatility windows.</div>
            <div class="a-tags">
              <span class="a-tag">line chart</span>
              <span class="a-tag">time-series</span>
              <span class="a-tag">/market_chart</span>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>

  <!-- Insights -->
  <div class="section" id="insights">
    <div class="section-header">
      <span class="section-num">05</span>
      <span class="section-title">Key Insights</span>
    </div>
    <div class="insights-grid">
      <div class="insight-card c1">
        <div class="insight-label">CORRELATION</div>
        <div class="insight-text">Market capitalization shows strong positive correlation with trading volume across all major assets.</div>
      </div>
      <div class="insight-card c2">
        <div class="insight-label">VOLATILITY</div>
        <div class="insight-text">High-volume assets tend to exhibit greater price stability relative to low-liquidity micro-caps.</div>
      </div>
      <div class="insight-card c3">
        <div class="insight-label">TREND</div>
        <div class="insight-text">Bitcoin displays short-term volatility clusters but maintains clear directional trend behavior over 30-day windows.</div>
      </div>
    </div>
  </div>

  <!-- Quickstart -->
  <div class="section" id="quickstart">
    <div class="section-header">
      <span class="section-num">06</span>
      <span class="section-title">Quickstart</span>
    </div>

    <div class="code-block">
      <div class="code-head">
        <span class="code-lang">BASH</span>
        <button class="code-copy" onclick="copyCode(this, 'bash-code')">copy</button>
      </div>
      <pre id="bash-code"><span class="c-comment"># Clone the repository</span>
<span class="c-cmd">git clone</span> https://github.com/your-username/crypto-market-analytics.git
<span class="c-cmd">cd</span> crypto-market-analytics

<span class="c-comment"># Create virtual environment</span>
<span class="c-cmd">python -m venv</span> .venv
<span class="c-cmd">source</span> .venv/bin/activate  <span class="c-comment"># Windows: .venv\Scripts\activate</span>

<span class="c-comment"># Install dependencies</span>
<span class="c-cmd">pip install</span> -r requirements.txt

<span class="c-comment"># Launch Jupyter</span>
<span class="c-cmd">jupyter notebook</span> crypto_analytics.ipynb</pre>
    </div>

    <div class="code-block" style="margin-top: 12px;">
      <div class="code-head">
        <span class="code-lang">PYTHON — FETCH SNAPSHOT</span>
        <button class="code-copy" onclick="copyCode(this, 'py-code')">copy</button>
      </div>
      <pre id="py-code"><span class="c-kw">import</span> requests
<span class="c-kw">import</span> pandas <span class="c-kw">as</span> pd

url <span class="c-kw">=</span> <span class="c-str">"https://api.coingecko.com/api/v3/coins/markets"</span>
params <span class="c-kw">=</span> {
    <span class="c-str">"vs_currency"</span>: <span class="c-str">"usd"</span>,
    <span class="c-str">"order"</span>:       <span class="c-str">"market_cap_desc"</span>,
    <span class="c-str">"per_page"</span>:     <span class="c-str">10</span>,
    <span class="c-str">"price_change_percentage"</span>: <span class="c-str">"24h"</span>
}

response <span class="c-kw">=</span> requests.<span class="c-fn">get</span>(url, params<span class="c-kw">=</span>params)
df       <span class="c-kw">=</span> pd.<span class="c-fn">DataFrame</span>(response.<span class="c-fn">json</span>())
<span class="c-fn">print</span>(df[[<span class="c-str">"name"</span>, <span class="c-str">"current_price"</span>, <span class="c-str">"market_cap"</span>, <span class="c-str">"total_volume"</span>]])</pre>
    </div>
  </div>

  <!-- Footer -->
  <div class="footer">
    <div class="footer-left">crypto-market-analytics · MIT License · 2024</div>
    <div class="footer-right">
      <a class="footer-link" href="https://www.coingecko.com/api/documentation" target="_blank">API Docs</a>
      <a class="footer-link" href="https://github.com" target="_blank">GitHub</a>
      <a class="footer-link" href="#quickstart">Quickstart ↑</a>
    </div>
  </div>

</div>

<script>
function copyCode(btn, id) {
  const el = document.getElementById(id);
  const text = el.innerText;
  navigator.clipboard.writeText(text).then(() => {
    btn.textContent = 'copied!';
    btn.style.color = '#3fb950';
    btn.style.borderColor = '#3fb950';
    setTimeout(() => {
      btn.textContent = 'copy';
      btn.style.color = '';
      btn.style.borderColor = '';
    }, 2000);
  });
}
</script>
</body>
</html>
