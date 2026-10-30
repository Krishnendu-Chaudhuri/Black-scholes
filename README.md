# Black-Scholes Live Pricing — Indian Stocks (NSE)

A production-ready Jupyter notebook that pulls **live market data** for Indian equities via `yfinance` and runs a complete **Black-Scholes-Merton** analysis (prices + Greeks) with heatmaps, sensitivity plots, an interactive dashboard, and batch pricing.

---

## Features

| Feature | Description |
|---------|-------------|
| **Live data** | Spot price and 252-day historical volatility from NSE / BSE via `yfinance` |
| **Black-Scholes engine** | European call & put prices plus all major Greeks (Δ, Γ, Vega, Θ, ρ) |
| **Configurable inputs** | Strike, tenor, risk-free rate (default India 10Y / RBI proxy ≈ 6.75%), volatility multiplier |
| **Visuals** | Price curves vs spot, volatility heatmaps (call & put), option-chain style grid |
| **Interactive dashboard** | `ipywidgets` UI to pick popular NSE stocks or type a custom ticker and re-price instantly |
| **Batch mode** | Price a watchlist of stocks at once (ATM or custom moneyness) |
| **Ticker support** | NSE: `SYMBOL.NS` · BSE: `SYMBOL.BO` (auto-appends `.NS` if missing) |

---

## Requirements

```bash
pip install yfinance numpy scipy pandas matplotlib seaborn ipywidgets
```

- Python ≥ 3.9 recommended  
- Jupyter / VS Code / Google Colab  
- Internet access (for live quotes)

---

## Quick Start

1. Open `BlackScholes_Live_Indian_Stocks.ipynb`.
2. Run the install/import cell (uncomment the `pip` line if needed).
3. In **Section 4**, set the ticker (default: `RELIANCE.NS`) and risk-free rate.
4. Execute cells sequentially — live data is fetched, the model is calibrated, and plots/tables are generated.
5. (Optional) Use the interactive dashboard in **Section 10** or the batch watchlist in **Section 11**.

### Example snapshot (illustrative)

```
=======================================================
  RELIANCE INDUSTRIES LTD  (RELIANCE.NS)
  As of           : 2026-10-29
  Spot (Close)    : ₹ 1,167.40
  Hist. Vol (ann.): 21.37%   (252 trading days)
  Risk-free rate  : 6.75%
=======================================================
```

---

## Notebook Structure

| Section | Content |
|---------|---------|
| 1 | Install / import libraries |
| 2 | `BlackScholes` class (prices + Greeks) |
| 3 | Live-data helpers (`fetch_stock_data`, popular NSE list) |
| 4 | Choose stock & pull live data |
| 5–6 | Price a single option & print Greeks summary |
| 7–8 | Price curves and spot–vol heatmaps |
| 9 | Theoretical option-chain grid (multiple strikes & tenors) |
| 10 | Interactive live dashboard (`ipywidgets`) |
| 11 | Batch pricing for a watchlist |
| 12 | Notes & caveats |

---

## Black-Scholes Model

European option (no dividends):

\[
\begin{aligned}
d_1 &= \frac{\ln(S/K) + (r + \tfrac12\sigma^2)T}{\sigma\sqrt{T}}, \quad
d_2 = d_1 - \sigma\sqrt{T} \\
C &= S\,N(d_1) - K e^{-rT} N(d_2) \\
P &= K e^{-rT} N(-d_2) - S\,N(-d_1)
\end{aligned}
\]

Greeks returned by the class:

- **Delta** (call / put)  
- **Gamma**  
- **Vega** (per 1% vol)  
- **Theta** (per calendar day)  
- **Rho** (per 1% rate)

---

## Popular NSE Tickers Included

`RELIANCE`, `TCS`, `INFY`, `HDFCBANK`, `ICICIBANK`, `SBIN`, `BHARTIARTL`, `ITC`, `HINDUNILVR`, `LT`, `AXISBANK`, `KOTAKBANK`, `BAJFINANCE`, `ASIANPAINT`, `MARUTI`, `TATAMOTORS`, `SUNPHARMA`, `WIPRO`, `HCLTECH`, `NTPC`

You can also type any valid `SYMBOL.NS` or `SYMBOL.BO`.

---

## Important Caveats

| Topic | Note |
|-------|------|
| **Volatility** | Uses **historical** (realized) vol. Market implied vol from the NSE option chain will typically differ (smile/skew). |
| **Risk-free rate** | Default 6.75%. Update `RISK_FREE` to the latest India 10Y G-Sec or RBI repo rate. |
| **Dividends** | Model assumes zero dividend yield. For high-dividend names consider subtracting expected yield or switching to Black-Scholes-Merton with continuous yield \(q\). |
| **Style** | NSE equity options are European-style; the BS formula is appropriate. |
| **Liquidity** | Theoretical prices ignore bid–ask spreads and market impact. |
| **Data lag** | `yfinance` closes can be delayed; true real-time requires a paid feed. |

---

## Suggested Extensions

- Add continuous dividend yield \(q\) (Black-Scholes-Merton).  
- Pull implied volatility from the live NSE option chain and compare with historical vol.  
- Surface plots of price / Greeks vs \(S\) and \(\sigma\).  
- Export batch results to CSV / Excel for further analysis.  
- Replace historical vol with GARCH or EWMA estimates.

---

## License & Disclaimer

This notebook is for **educational and research purposes only**. It is **not** investment advice. Always cross-check with official exchange data and a licensed broker before trading.

---


