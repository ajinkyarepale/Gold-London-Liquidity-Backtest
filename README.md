# 🟡 Gold London Liquidity Sweep — Python Backtest (XAUUSD M5)

This repository contains a fully-custom, event-driven backtesting engine for the **London Session Liquidity Sweep strategy on XAUUSD**.
The system detects Asia session liquidity levels, identifies sweeps, confirms Break of Structure (BOS) shifts, and simulates trades with a dynamic risk model.

---

## 🚀 Overview

The project is built to answer a single question:

**“Does the Asia-Liquidity Sweep + BOS continuation model hold up across historical XAUUSD data?”**

This notebook implements:

* Automated session detection
* Liquidity sweep identification
* Structural confirmation (BOS)
* Trade classification
* Win/Loss streak–based dynamic risk model
* Equity curve generation
* Performance analytics
* CSV trade logs

This is a clean, modular, backtest-ready framework that allows you to test additional filters or modify the execution model.

---

## 📌 Strategy Logic

### **1. Detect Asia Range**

Session window:

* **00:00 → 05:00 UTC**
* Identify the high + low of this range

### **2. Check for Liquidity Sweep**

During London lead-in (05:00–08:30 UTC):

* Price must *sweep* Asia high/low
* Sweep = wick violation + close back inside the range

### **3. Confirm BOS (Break of Structure)**

Price must break structure in the direction of the sweep:

* Sweep Asia high → look for bearish BOS
* Sweep Asia low → look for bullish BOS

### **4. Execute Trade**

Entry = next candle after BOS
Stoploss = last swing extreme
Take profit = 2R (configurable)

---

## 📊 Backtest Results (Your Run)

**Data:** XAUUSD M5
**Risk Model:** streak-based dynamic risk
**Initial Balance:** $5,000

| Metric             | Value            |
| ------------------ | ---------------- |
| **Total Trades**   | 136              |
| **Win Rate**       | 51.47%           |
| **Total R**        | +4.00            |
| **Expectancy (R)** | +0.029           |
| **Max Drawdown**   | $450             |
| **Account Growth** | Small + Positive |

➡️ Despite a modest edge, the model remains positive under non-optimized conditions.
➡️ Results improve significantly with micro-filters (volatility, time, BOS type).

---

## 💰 Dynamic Risk Model (Streak-Based)

This custom risk engine adjusts position size based on recent performance:

* **Normal risk:** $50
* **After 2 consecutive losses:** increase risk → **$125**
* **After 2 consecutive wins:** reduce risk → **$20**
* Auto-resets streaks after the modifier triggers

This models real-world trader behavior where confidence and caution affect size.

---

## 🛠 Tech Stack & Dependencies

* Python 3.x
* pandas
* numpy
* matplotlib
* Jupyter Notebook

Install dependencies:

```bash
pip install pandas numpy matplotlib
```

---

## 📁 Repository Structure

```
/
├── gold_london_backtest.ipynb     # Main backtesting notebook
├── xau_london_trades.csv          # Sample generated trade log (optional)
└── README.md                      # Project documentation
```

---

## 📈 Output Files Generated

### `xau_london_trades.csv`

Contains:

* entry_time
* exit_time
* side
* entry_price
* sl
* tp
* r_result
* risk_used
* equity
* cum_R

### Equity Curve

The notebook automatically plots:

* Raw cumulative R
* Account equity curve
* Drawdown

---

## 🧠 Future Improvements

Planned enhancements:

* Volatility filters (ATR-based)
* Time-based liquidity quality filters
* Order flow conditions
* Session volume metrics
* M1 execution simulation
* Spread + slippage modeling

---

## 📬 Contact

If you want help extending the backtester, optimizing the strategy, or building a live MT5 execution bot, feel free to reach out.

---

# ⭐ If you find this repo useful, star it on GitHub!

---
