# Market Risk & Value at Risk (VaR) Simulator

End-to-end market risk project developed in **Python** to analyze a multi-asset portfolio using Value at Risk, Expected Shortfall, backtesting and stress testing.

The project evaluates market risk across equity, fixed-income, commodity and FX exposures.

---

## Project Objective

The objective is to build a practical market-risk framework capable of:

- Constructing a diversified multi-asset portfolio
- Measuring daily portfolio P&L
- Estimating Value at Risk using multiple methodologies
- Estimating Expected Shortfall
- Comparing model assumptions
- Backtesting VaR estimates
- Applying the Kupiec unconditional coverage test
- Evaluating severe hypothetical market shocks

---

## Portfolio

The portfolio has an illustrative value of:

**USD 1,000,000**

and includes:

| Asset | Exposure | Weight |
|---|---|---:|
| SPY | U.S. Equities | 30% |
| QQQ | Technology Equities | 20% |
| TLT | Long-duration U.S. Treasuries | 25% |
| GLD | Gold | 15% |
| EUR/USD | FX Exposure | 10% |

Historical market data was obtained using `yfinance`.

---

## Methodology

The project includes:

1. Market data collection
2. Price alignment across asset classes
3. Daily return calculation
4. Portfolio construction
5. Historical VaR
6. Parametric VaR
7. Monte Carlo VaR
8. Historical and Parametric Expected Shortfall
9. Rolling VaR backtesting
10. Kupiec unconditional coverage test
11. Hypothetical stress testing

---

## Value at Risk Results

Three one-day VaR methodologies were compared.

| Method | VaR 95% | VaR 99% |
|---|---:|---:|
| Historical | $11,657 | $17,851 |
| Parametric | $11,476 | $16,360 |
| Monte Carlo | $11,505 | $16,407 |

The three methods produced similar estimates at the 95% confidence level.

At the 99% confidence level, Historical VaR was materially higher than the Parametric and Monte Carlo estimates.

This suggests that historical portfolio returns contain more severe tail losses than those implied by the normal-distribution assumptions used by the parametric framework.

---

## Expected Shortfall

Expected Shortfall was used to estimate the average loss once the VaR threshold is exceeded.

| Method | VaR 95% | ES 95% | VaR 99% | ES 99% |
|---|---:|---:|---:|---:|
| Historical | $11,657 | $16,201 | $17,851 | $23,881 |
| Parametric | $11,476 | $14,471 | $16,360 | $18,789 |

Historical Expected Shortfall was significantly higher than the parametric estimate in the extreme tail.

At the 99% confidence level:

- Historical VaR: approximately **$17.9K**
- Historical Expected Shortfall: approximately **$23.9K**

This demonstrates that losses beyond the VaR threshold can be materially larger than the VaR estimate itself.

---

## VaR Backtesting

A rolling **250-day Historical VaR** was evaluated over:

**1,217 backtesting observations**

The VaR for each day was estimated exclusively using information available before that day.

### 95% VaR

- Expected exceptions: 60.85
- Observed exceptions: 72
- Exception rate: **5.92%**
- Kupiec p-value: **0.154**

### 99% VaR

- Expected exceptions: 12.17
- Observed exceptions: 18
- Exception rate: **1.48%**
- Kupiec p-value: **0.117**

Although observed exception rates were somewhat higher than theoretical expectations, both Kupiec p-values were above the 5% significance level.

Therefore, the null hypothesis of correct unconditional VaR coverage was not rejected.

---

## Stress Testing

Four hypothetical scenarios were applied to the portfolio.

| Scenario | Portfolio Return | Portfolio P&L |
|---|---:|---:|
| Broad Market Stress | -10.20% | **-$102,000** |
| Rate Shock | -7.20% | -$72,000 |
| Equity Selloff | -6.95% | -$69,500 |
| Risk-Off Flight | -3.15% | -$31,500 |

The most severe scenario generated a loss of:

**$102,000**

equivalent to:

**10.2% of portfolio value**

For comparison:

- Historical VaR 99%: **$17.9K**
- Historical Expected Shortfall 99%: **$23.9K**
- Worst stress scenario: **$102K**

This highlights the difference between statistical tail-risk measures and deliberately severe stress scenarios.

---

## Key Findings

Several important conclusions emerged from the analysis:

- Historical, Parametric and Monte Carlo VaR produced similar 95% risk estimates.
- Historical VaR and Expected Shortfall were higher in the extreme 99% tail.
- Normal-distribution assumptions understated the severity of historical tail losses.
- Rolling Historical VaR produced slightly more exceptions than theoretically expected.
- The Kupiec test did not reject VaR coverage at the 5% significance level.
- Stress testing generated losses substantially larger than standard VaR and Expected Shortfall measures.

---

## Project Structure

```text
market-risk-var-simulator/
│
├── data/
│   ├── raw/
│   └── processed/
│       ├── market_prices.csv
│       ├── daily_returns.csv
│       └── portfolio_returns.csv
│
├── notebooks/
│   ├── 01_market_data_and_portfolio.ipynb
│   ├── 02_var_models.ipynb
│   ├── 03_expected_shortfall.ipynb
│   ├── 04_backtesting.ipynb
│   └── 05_stress_testing.ipynb
│
├── reports/
│   └── figures/
│
├── src/
├── .gitignore
├── requirements.txt
└── README.md
```

---

## Technologies

- Python
- Pandas
- NumPy
- SciPy
- Matplotlib
- yfinance
- Jupyter Notebook
- Git
- GitHub

---

## Installation

Clone the repository:

```bash
git clone <repository-url>
```

Move into the project directory:

```bash
cd market-risk-var-simulator
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## Limitations

This project is an analytical portfolio project and not a production market-risk engine.

Important limitations include:

- Historical correlations may not remain stable during market stress.
- Parametric VaR assumes approximately normally distributed returns.
- Monte Carlo simulation uses historical means and covariance estimates.
- The stress scenarios are hypothetical rather than calibrated regulatory scenarios.
- The portfolio assumes static weights.
- Transaction costs, liquidity risk and intraday market dynamics are not modeled.
- Interest-rate exposure is represented through TLT rather than a full duration-based fixed-income book.

---

## Potential Improvements

Future extensions could include:

- EWMA volatility
- GARCH volatility models
- Student-t Monte Carlo simulation
- Historical crisis scenarios
- Component VaR and Marginal VaR
- Duration and DV01 analysis
- FX sensitivity analysis
- Liquidity-adjusted VaR
- Power BI risk dashboard
- Dynamic portfolio rebalancing
- Basel-style traffic-light backtesting

---

## Author

**Airam Fortunato**

Financial Engineering student focused on Risk Management, Data Analytics, Data Science and Quantitative Finance.