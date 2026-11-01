# NVDA Dynamic Hedging Strategy

A quantitative, event-driven hedging strategy implemented in **Blueshift** designed to dynamically hedge a long position in NVIDIA (**NVDA**) using the S&P 500 ETF (**SPY**).

---

## Strategy Overview

* **Asset:** Long NVDA (`NVDA`)
* **Hedge:** Short/Dynamic position in SPY (`SPY`)
* **Frequency:** Daily rebalancing (market close)
* **Lookback Window:** 60 trading days for rolling OLS regression

---

## How It Works

1. **Data Collection:** Pulls 60 days of daily close prices for both NVDA and SPY via Blueshift's historical data API (`data.history`).
2. **Beta Estimation:** Computes daily returns and runs an Ordinary Least Squares (OLS) regression (`statsmodels`) to estimate the sensitivity ($\beta$) of NVDA relative to the SPY benchmark.
3. **Dynamic Positioning:** Automatically sizes portfolio weights to maintain a long exposure on NVDA combined with a dynamic short hedge proportional to its rolling beta (`-0.5 * beta`).


---

## Requirements & Dependencies

* `blueshift.api`
* `numpy`
* `statsmodels`