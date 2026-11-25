# Synthetic Tech ETF — Moving Average Research

A Python notebook exploring moving averages and a simple trading strategy on a synthetic basket of six technology and technology-related stocks: AAPL, MSFT, NVDA, AMZN, GOOGL and META.

The project compares a 5/20-day moving-average strategy with buying and holding the same basket. It is an exploratory learning project, with the current calculations and charts saved in the notebook.

## What the notebook does

1. Downloads daily prices and stock-split events from Yahoo Finance using `yfinance`, requesting data from 1 January 2010 onward.
2. Keeps dates with closing prices for all six stocks, multiplies each price series by its cumulative split factor, and sums the series into a synthetic basket price.
3. Calculates 5-, 10-, 20- and 200-day simple moving averages and plots the price history in two-year sections.
4. Sets a long-or-cash trend indicator according to whether the 5-day average is above the 20-day average.
5. Compares strategy value with buy and hold, starting with $10,000, and reports total returns and the number of position changes.

## Run the notebook

Use Python with Jupyter, or VS Code with its Python and Jupyter extensions.

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
jupyter lab
```

On Windows, activate the environment with `.venv\Scripts\activate` instead. Open [`moving average crossover.ipynb`](moving%20average%20crossover.ipynb), select the environment as the notebook kernel, and run the cells in order. Internet access is required for the price download. The first cell also installs `yfinance`.

## Current assumptions and limitations

- The basket is a constructed price series, not a listed ETF or an equal-weight portfolio. Its split-factor scaling determines the relative contribution of each stock.
- Requiring data for all six stocks means the usable history starts later than the requested 2010 start date. The six names are selected retrospectively, so the exercise does not address survivorship or stock-selection bias.
- The position uses the trend indicator from two trading rows earlier (`shift(2)`). Returns use daily close-to-close changes; the notebook does not model individual trade fills.
- Each position change incurs an assumed cost of 0.1% of portfolio value. Cash earns no interest, dividends are not credited, and there is no separate model for spreads or slippage. The buy-and-hold comparison has no transaction costs.
- Data is downloaded again on each run, with no fixed end date or archived input snapshot. Dependencies are not pinned, so saved results may differ from a later run.
- The notebook has no separate out-of-sample evaluation. The charts and historical comparison do not establish predictive performance.

## Files

- `moving average crossover.ipynb` — research code, explanation and saved charts.
- `requirements.txt` — packages needed to run the notebook.
- `.gitignore` — excludes local environments, caches, editor settings, credentials and local data directories.
