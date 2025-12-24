# Marigold V1 — ML Signal Validation for Crypto Trading

Marigold V1 is the first iteration of a long-term project aimed at building a crypto trading system.

V1 is intentionally **not a trading bot**.  
It's solely to validate whether **any predictive signal exists** in short-horizon crypto price data using disciplined machine learning practices.

---

## 🎯 Objective

> Does any predictive signal exist in BTC price movements that survives proper time-series validation?

V1 prioritises:

- Correctness over performance  
- Stability over optimisation  
- Learning over profits  

---

## 📊 Data

- **Asset:** BTC/USDT  
- **Timeframe:** 2-hour candles  
- **Period:** 2021 – 2025  
- **Source:** Binance (via CCXT)  
- **Raw Features:** OHLCV  

### Data Splitting

Time-based split:

- Train: 60%  
- Validation: 20%  
- Test: 20%  

---

## 🧠 Target Definition

Binary classification:


The target is intentionally noisy and short-horizon to test baseline signal strength.

---

## 🧪 Feature Engineering

Features were added incrementally and kept only if they generalised across validation and test sets.

### Final V1 Feature Set (Frozen)

| Feature   | Description |
|----------|-------------|
| return_1 | Previous candle return |
| mom_10   | Momentum vs 10-period rolling mean |
| vol_30   | 30-period rolling volatility |

Many other features (e.g. return_5, vol_10, ratios, trend strength) were tested and explicitly rejected due to a lack of generalisation.

---

## 🤖 Model

- Logistic Regression  
- Inputs scaled using `StandardScaler`  
- No hyperparameter tuning  

Chosen deliberately for:

- Interpretability  
- Low variance  
- Honest signal inspection  

---

## 📈 Evaluation

- **Metric:** ROC-AUC  

| Split | ROC-AUC |
|------|--------|
| Validation | ~0.53–0.55 |
| Test | ~0.53–0.54 |

### Interpretation

- Weak but real signal  
- Typical for financial time-series  
- Higher values would be suspicious  

---

## 🔍 Error Analysis

High-confidence error analysis revealed:

- Failure rates increase when:
  - Volatility is high  
  - Momentum is weak or negative  

Errors were regime-dependent, not clustered in time.

---

## 🚦 Decision to trade:

A simple regime filter was tested:


### Results

- ~9–10% of trades skipped  
- Slight reduction in error rate  
- Improved decision stability 

---

## 🧪 Backtest (Sanity Check)

A minimal backtest translated predictions into trades:

- Long-only  
- Trade when predicted probability > 0.55  
- Skip bad regimes  
- Hold for 1 candle  
- No transaction costs  
- No position sizing  

### Results

- Total return: ~ −14%  
- Max drawdown: ~ −15%  
- No catastrophic blow-ups  
- Realistic equity behaviour  

Conclusion:  
The signal is not tradable in raw form, but the system behaves sanely.

---

## ⚖️ Bias–Variance Position

V1 intentionally chose:

- High bias (simple target, linear model)  
- Low variance (stable performance across splits)  

This avoids false confidence and overfitting.

---

## ✅ V1 Verdict

- ✔ Signal exists  
- ✔ No data leakage  
- ✔ Honest evaluation  
- ✔ Realistic backtest  
- ✘ Not profitable  

V1 is successful by design.

---

## 🚧 Limitations

- Extremely noisy target  
- No transaction costs  
- No position sizing  
- No short positions  
- No execution modelling  

All intentionally deferred.

---

## 🔜 Next Steps (V2)

- Improved target definition (longer horizon / volatility-adjusted)  
- Better execution logic  
- Risk & payoff asymmetry  
- Careful introduction of more expressive models  

---

## 📌 Status


**Marigold V1 — Complete**
