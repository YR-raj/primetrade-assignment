# Trader Performance vs Market Sentiment — Primetrade.ai Assignment

## 📌 Objective

This project analyzes how Bitcoin market sentiment (Fear/Greed Index) relates to trader behavior and performance on Hyperliquid. The goal is to identify meaningful patterns that can inform smarter trading strategies.

---

## 📂 Data Sources

Two datasets were used:

1. **Fear & Greed Index (`fear_greed_index.csv`)**

   * Daily market sentiment labels (Extreme Fear, Fear, Neutral, Greed, Extreme Greed)

2. **Historical Trader Data (`historical_data.csv`)**

   * Contains trade-level records including:

     * account, coin, execution price
     * size (tokens & USD), side (BUY/SELL)
     * timestamps, leverage, closedPnL, fees, etc.

---

## 🛠️ Setup & How to Run

### Requirements

Create and activate your conda environment:

```bash
conda create -n primetrade python=3.10 -y
conda activate primetrade
pip install pandas numpy matplotlib seaborn jupyter
```

### Run the analysis

```bash
jupyter notebook notebooks/trader_sentiment_analysis.ipynb
```

Run all cells sequentially.

---

## 📊 Outputs (included in EDA_images folder)

* `pnl_by_sentiment.png` – Average PnL across Fear vs Greed days
* `behavior_by_sentiment.png` – Trades, leverage, and long/short bias vs sentiment
* `leverage_segment_pnl.png` – High vs Low leverage performance
* `frequency_segment_pnl.png` – Frequent vs Infrequent trader performance

---

## 🧠 Methodology (Summary)

1. **Data Cleaning**

   * Converted timestamps to datetime
   * Aligned both datasets at a **daily level**
   * Removed duplicates and handled missing values and Outliers

2. **Feature Engineering**

   * Computed:

     * Daily PnL per trader
     * Win rate
     * Average trade size
     * Average leverage
     * Number of trades per day
     * Long/short ratio

3. **Analysis**

   * Compared performance across sentiment regimes
   * Studied behavior changes with sentiment
   * Created three trader segments:

     * High vs Low leverage
     * Frequent vs Infrequent traders
     * Consistent vs Inconsistent traders

---

## 🔍 Key Insights

### Insight 1 — Sentiment vs Performance

* Market Sentiment does impact trader's performance
* When the market is greed, PnL is low, suggesting that trader might get too `aggressive` or `overconfident`.
* However, when it is fear, PnL is high, suggesting cautious behaviour of the trader.

### Insight 2 — Trader behaviour vs sentiment
* Trader trade `much` more during fear and `less` in greed days.
* Traders use `much higher leverage` when the market is greed, which explains why the `PnL` is low in greed.
* In Greed markets, traders are `long biased`, while in Fear markets they are more balanced. 

### Insight 3 — Leverage Risk
* **Low-leverage traders consistently outperform high-leverage traders**, especially during Fear periods, indicating that leverage amplifies downside risk more than upside gains.

### Insight 4 — Activity Matters in Fear
* During Fear days, **frequent traders significantly outperform infrequent traders**, implying that active risk management is beneficial in volatile markets.
* On average, Frequent Traders differ from Infrequent Traders by **`~133%`** across sentiment categories.

---

## 🎯 Strategy Recommendations

### **Strategy 1 — Adaptive Leverage Rule**

* **If sentiment = Fear or Extreme Fear → reduce leverage by 30–40%**
* Especially for high-leverage traders
* Rationale: low-leverage traders perform better in fear regimes.

### **Strategy 2 — Activity-Based Trading**

* **If sentiment = Fear → increase trading activity only for frequent traders**
* **If sentiment = Greed → reduce trading frequency for infrequent traders**
* Rationale: Frequent traders handle volatility better; infrequent traders perform poorly in panic markets.
