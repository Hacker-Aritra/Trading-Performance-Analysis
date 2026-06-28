# Trading-Performance-Analysis
End-to-end performance analysis of 92 live algo-trading trades across forex &amp; index markets — feature engineering, drawdown/risk metrics, and a 100K-iteration Monte Carlo simulation to project future outcomes


1. Prerequisites
bashpip install pandas numpy matplotlib scipy --break-system-packages
2. Folder setup
The scripts expect this structure (create the folders first):
bashmkdir -p project/data project/charts
cd project
unzip analysis_scripts.zip   # gives you project/scripts/
Your folder should look like:
project/
├── data/      ← CSVs land here
├── charts/    ← PNG charts land here
└── scripts/   ← the 6 .py files
3. Run the scripts in order
Each one depends on the output of the previous, so run them sequentially:
bashcd scripts

python3 01_generate_raw_data.py        # → data/raw_trade_history.csv
python3 02_feature_engineering.py      # → data/trades_enriched.csv
python3 03_performance_metrics.py      # → data/performance_metrics.json
python3 04_monte_carlo_simulation.py   # → data/monte_carlo_results.json + .npy files
python3 05_strategy_insights.py        # → data/strategy_insights.json
python3 06_generate_charts.py          # → charts/*.png (7 chart files)


4. To use your own real trade data instead of the synthetic set
Skip step 1 (01_generate_raw_data.py) and instead drop your own broker export into data/raw_trade_history.csv, matching these columns:
ticket, symbol, type, lots, open_time, close_time, open_price, close_price,
sl, tp, commission, swap, profit, net_profit, comment
Then run steps 2–6 as normal — everything downstream (feature engineering, metrics, Monte Carlo, charts) will regenerate against your real trades.
