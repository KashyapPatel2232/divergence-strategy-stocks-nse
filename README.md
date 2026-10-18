# NSE Divergence Strategy Stocks

An interactive Jupyter notebook for exploring NSE-listed equities with candlestick charts, volume, RSI, and price/RSI divergence markers.

![Example output: interactive NSE chart layout](the-great-estern-shipping-company-limit.png)

The preview above illustrates the chart layout. When you run the notebook, it fetches current history from NSE for the ticker you select.

## Features

- Fetches daily history from the ticker's NSE listing date.
- Adjusts historical prices for supported stock splits and bonus issues; adjusts share volumes for those share-count changes.
- Applies supported cash-dividend price adjustments. Corporate actions that cannot be safely interpreted (such as demergers) are not guessed; review the notebook's action messages and NSE disclosures.
- Aggregates candles to **Daily, Weekly, Monthly, 3 Months, 6 Months, and 12 Months**.
- Shows price, volume, and 14-period RSI in linked panels with synchronized date navigation.
- Compresses weekends and dates with no trading candle so market closures do not create long blank stretches.
- Marks bearish divergence at price/RSI swing highs and bullish divergence at swing lows, requiring a run of at least three consecutive matching pivots.
- Includes zoom, pan, hover details, a cross-panel cursor guide, and date-window controls.

## Requirements

- Python 3.11 or newer
- Internet access to retrieve NSE data and Plotly.js
- A Jupyter environment (JupyterLab is included in the requirements below)

## Setup and run

From a terminal:

```bash
git clone https://github.com/KashyapPatel2232/divergence-strategy-stocks-nse.git
cd divergence-strategy-stocks-nse

python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python -m ipykernel install --user --name nse-divergence --display-name "Python (NSE Divergence)"
jupyter lab nse_divergence_analyzer.ipynb
```

On Windows PowerShell, activate the environment with:

```powershell
.\.venv\Scripts\Activate.ps1
```

In the notebook:

1. Run the first cell to install the project requirements (or use the terminal setup above).
2. Set `SYMBOL` in the ticker cell to an NSE equity symbol, for example `GESHIP`, `TIPSMUSIC`, or `KSOLVES`.
3. Select the `Python (NSE Divergence)` kernel if Jupyter did not select it automatically.
4. Run the chart cell. It retrieves data and builds the interactive chart; allow time for older listings to download.
5. Use the candle-period buttons to change aggregation. Hover over the plot for values; zoom, pan, and use the date-window slider to inspect history.

The `SYMBOL` cell is the single ticker setting. The notebook fetches security metadata and daily prices from NSE; no API key is required. Requests can fail or be throttled if NSE is unavailable, the symbol is invalid, or the exchange changes its endpoints.

## Divergence notes

The notebook identifies local swing highs/lows using neighboring candles, matches nearby RSI pivots to price pivots, and marks runs of at least three consecutive highs or lows where price and RSI move in opposite directions. These are visual research annotations, not trading signals or a backtested strategy. Recent pivots need candles to their right to be confirmed.

## Data and corporate-action caveats

Data is retrieved at run time using [`jugaad-data`](https://github.com/jugaad-py/jugaad-data) and NSE endpoints. The notebook normalizes the exchange history dates and adjusts supported splits, bonus issues, and cash dividends. NSE descriptions can be ambiguous or incomplete; the notebook does not invent adjustments for unsupported corporate actions. Always verify adjusted series against official exchange/company disclosures before relying on them.

The chart uses the available trading candles to compress weekends and other non-trading dates. This is intended for visual analysis and does not replace an official exchange calendar.

## Disclaimer

This project is for educational and research use only. It is not investment, financial, or trading advice. Market data may be delayed, incomplete, revised, or unavailable. You are responsible for validating data, complying with NSE terms and applicable laws, and making your own decisions.
