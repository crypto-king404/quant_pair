# Quant Pairs Trading Framework

A fully end-to-end statistical arbitrage backtesting system for equity pairs, built in Python and Dockerized for reproducibility.  
Identify cointegrated pairs, generate z-score entry/exit signals, and evaluate performance via in-sample, out-of-sample and walk-forward tests.

---

## 📈 Features

- **Data Ingestion & Cleaning**  
  - Pulls daily OHLCV for S&P 500 tickers via your choice of API (Alpha Vantage, Tiingo, etc.)  
  - Adjusts for splits/dividends, forward-fills missing data, and stores as Parquet

- **Pair Selection & Cointegration**  
  - Filters by liquidity, groups by sector to reduce candidate space  
  - Runs Engle–Granger cointegration tests; selects pairs with p < 0.05  
  - Computes optimal hedge ratio β via OLS

- **Signal Generation**  
  - Calculates rolling mean and standard deviation of the spread  
  - Generates long/short/exit signals based on configurable z-score thresholds  
  - Supports parameter sweeps for lookback windows and entry/exit levels

- **Backtesting Engine**  
  - Built on [Backtrader](https://www.backtrader.com/)  
  - Models slippage and per-share commission  
  - Runs in-sample and out-of-sample backtests with detailed trade logs

- **Robustness & Analysis**  
  - Sensitivity and stress tests (slippage, threshold variation)  
  - Walk-forward testing across rolling windows  
  - Risk attribution by pair, turnover analysis, drawdown charts  

- **Deployment & Reproducibility**  
  - Dockerized environment for “one-click” execution  
  - CLI interface:  
    ```bash
    docker run --rm quant_pairs \
      --start 2015-01-01 --end 2022-12-31 \
      --lookback 60 --entry 1.0 --exit 0.0
    ```
  - Generates equity curves, performance metrics, and CSV/PNG outputs  

---

## 🚀 Quick Start

1. **Clone this repository**  
   ```bash
   git clone https://github.com/crypto-king404/quant-pairs-trading.git
   cd quant-pairs-trading
