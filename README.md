# Momentum Factor Model

Backtesting the classic momentum strategy on S&P 500 stocks (2016-2025).

## Overview

This project implements the well-documented momentum factor: stocks that have performed well recently tend to continue performing well, and vice versa. The strategy ranks all S&P 500 stocks by their trailing 11-month returns (skipping the most recent month to avoid short-term reversal), then goes long the top decile and short the bottom decile.

## Key Findings

- **Pre-COVID (2016-2020):** Strategy worked as expected, compounding to ~$1.25 on $1 invested
- **March 2020:** Momentum crash — the strategy suffered a ~45% drawdown as market leadership violently reversed
- **Post-COVID:** Strategy struggled to recover, demonstrating the tail risk that momentum is known for
- **Long-only variant:** Simply holding winners (no short position) returned ~6x over the period

This matches academic research on momentum: it works until it doesn't, and when it fails, it fails hard at market inflection points.

## Methodology

1. **Data:** Daily price data for S&P 500 constituents pulled via yfinance, converted to monthly
2. **Momentum signal:** 11-month cumulative return, lagged by 1 month
3. **Portfolio construction:** Rank stocks into deciles each month; long top decile, short bottom decile
4. **Rebalancing:** Monthly

## Files

- `momentum.ipynb` — Main notebook with data pull, analysis, and visualizations
- `requirements.txt` — Python dependencies

## Setup

```bash
# Clone the repo
git clone https://github.com/YOUR_USERNAME/momentum-factor-model.git
cd momentum-factor-model

# Create virtual environment
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Run the notebook
jupyter notebook momentum.ipynb
```

Note: The initial data pull takes ~10 minutes for 500 stocks × 10 years of daily data.

## Results

![Momentum Strategy vs S&P 500](charts/momentum_vs_spy.png)

## Lessons Learned

- **Momentum crashes are real:** The COVID reversal wiped out years of gains in weeks
- **Data quality matters:** Attempted to expand to Russell 3000 but encountered survivorship bias and garbage data that overwhelmed the signal
- **Long-only outperformed:** In a bull market, the short leg is a drag — you're paying for insurance you don't need

## Future Improvements

- Industry-neutral momentum (rank within sectors to avoid concentration)
- Add risk metrics: Sharpe ratio, max drawdown, Sortino ratio
- Multi-factor model combining momentum with value or quality

## References

- Jegadeesh, N., & Titman, S. (1993). "Returns to Buying Winners and Selling Losers"
- Daniel, K., & Moskowitz, T. (2016). "Momentum Crashes"