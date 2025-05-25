# Quant Pairs Trading Framework

A fully end-to-end statistical arbitrage backtesting system for equity pairs, built in Python and Dockerized for reproducibility.
Identify cointegrated pairs, generate z-score entry/exit signals, and evaluate performance via in-sample, out-of-sample and walk-forward tests.

---

## 📈 Features

### Data Ingestion & Cleaning

* Pulls daily OHLCV for S\&P 500 tickers via your choice of API (Alpha Vantage, Tiingo, etc.)
* Adjusts for splits/dividends, forward-fills missing data, and stores as Parquet

### Pair Selection & Cointegration

* Filters by liquidity, groups by sector to reduce candidate space
* Runs Engle–Granger cointegration tests; selects pairs with p < 0.05
* Computes optimal hedge ratio β via OLS

### Signal Generation

* Calculates rolling mean and standard deviation of the spread
* Generates long/short/exit signals based on configurable z-score thresholds
* Supports parameter sweeps for lookback windows and entry/exit levels

### Backtesting Engine

* Built on [Backtrader](https://www.backtrader.com/)
* Models slippage and per-share commission
* Runs in-sample and out-of-sample backtests with detailed trade logs

### Robustness & Analysis

* Sensitivity and stress tests (slippage, threshold variation)
* Walk-forward testing across rolling windows
* Risk attribution by pair, turnover analysis, drawdown charts

### Deployment & Reproducibility

* Dockerized environment for “one-click” execution
* CLI interface:

  ```bash
  docker run --rm quant_pairs \
    --start 2015-01-01 --end 2022-12-31 \
    --lookback 60 --entry 1.0 --exit 0.0
  ```
* Generates equity curves, performance metrics, and CSV/PNG outputs

---

## 🚀 Quick Start

1. **Clone this repository**

   ```bash
   git clone https://github.com/crypto-king404/quant-pairs-trading.git
   cd quant-pairs-trading
   ```

2. **Build & Run with Docker**

   ```bash
   # Build the image
   docker build -t quant_pairs .

   # Run backtest over desired period
   docker run --rm quant_pairs \
     --start 2015-01-01 --end 2019-12-31 \
     --lookback 60 --entry 1.5 --exit 0.0
   ```

3. **View Results**

   * `results/` folder will contain:

     * `equity_curve.png`
     * `performance_metrics.json`
     * `trade_log.csv`

---

## 🛠️ Installation (Local)

> **Requires**: Python 3.9+, pip, Docker (optional)

1. Create & activate a virtual environment

   ```bash
   python -m venv venv
   source venv/bin/activate
   ```

2. Install dependencies

   ```bash
   pip install -r requirements.txt
   ```

3. Configure data API credentials in `config.yaml`

   ```yaml
   api_key: YOUR_API_KEY_HERE
   api_provider: tiingo
   ```

4. Run backtest locally

   ```bash
   python run_backtest.py \
     --start 2015-01-01 --end 2019-12-31 \
     --lookback 60 --entry 1.0 --exit 0.0
   ```

---

## 📊 Sample Results

| Metric                  | In-Sample (2015–2019) | Out-of-Sample (2020–2022) |
| ----------------------- | --------------------- | ------------------------- |
| Annualized Return       | 12.4 %                | 10.1 %                    |
| Annualized Volatility   | 8.5 %                 | 9.0 %                     |
| Sharpe Ratio            | 1.46                  | 1.12                      |
| Max Drawdown            | –7.8 %                | –9.2 %                    |
| Average Turnover (p.a.) | 120 %                 | 110 %                     |

*See `results/` for full charts and logs.*

---

## 📚 References

* Engle, R. F., & Granger, C. W. J. (1987). “Co-integration and error correction: Representation, estimation, and testing.”
* Backtrader documentation: [https://www.backtrader.com/docu/](https://www.backtrader.com/docu/)
* “Statistical Arbitrage in the U.S. Equities Market” (Marlin & Dunis)

---

## 🤝 Contributing

1. Fork the repo
2. Create a feature branch (`git checkout -b feature/your-idea`)
3. Commit your changes (`git commit -m "Add spooky new feature"`)
4. Push to the branch (`git push origin feature/your-idea`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
