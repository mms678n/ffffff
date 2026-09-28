# XAUUSD AI Trading Intelligence — Complete n8n Project

This bundle is **signal-only** and contains no broker/MT5 order execution.

## Import order
1. 00 Bootstrap Data Tables
2. 01 Core Pipeline
3. 01A Economic Calendar Collector
4. 02 Signal Tracker
5. 03 Performance Engine
6. 04A Historical News Builder
7. 04B Historical News AI Classifier
8. 04 Backtesting Engine
9. 05 Data Quality Monitor
10. 06 Error Handler + Admin Alert
11. 07 Dashboard
12. 07B Dashboard Data API
13. 08 Strategy Research Optimizer
14. 09 Test Harness

Run workflow 00 once first.

## n8n Cloud variables
Create Project Variables: `TWELVEDATA_API_KEY`, `NEWSAPI_KEY`, `OPENROUTER_API_KEY`, `OPENROUTER_MODEL`, `TELEGRAM_BOT_TOKEN`, `TELEGRAM_CHAT_ID`, `TELEGRAM_ADMIN_CHAT_ID`, `ECON_CALENDAR_API_KEY`.

For production, replace variable-backed secrets with n8n Credentials where practical. NewsAPI supports API-key headers and the project uses that pattern.

## One-time setup
- Assign workflow 06 as the Error Workflow in the settings of the production workflows.
- Run 09 and confirm `PASSED`.
- Run 05 and confirm market data is `DATA_OK`.
- Run 04A to seed historical headlines before historical research.
- Run 04 and verify `lookahead_bias_check = PASSED`.
- Activate schedules only after manual tests.

## Strategy score
Trend 20 + Structure 20 + Liquidity 15 + Momentum 10 + News 20 + Correlation 10 + Session 5 = 100.

BUY/SELL also requires confluence, structure, RR, market data, news and AI gates. Missing critical inputs means WAIT/no delivery.

## Dashboard
Activate workflow 07 and open its production webhook `/webhook/xauusd-dashboard`.

## Existing Phase 1
The bundle uses `xauusd_signals_v2`, so it does not overwrite your existing `xauusd_signals`.

No profitability or win rate is guaranteed. Backtests are research only.

## Extended correlation and macro layer
Core v2.1 collects 1m/5m/15m/30m/1h/4h/1d XAU data and optional DXY, US10Y, XAG, VIX and BTC confirmations. Economic-calendar events are collected separately and high-impact events inside the blackout window block signal delivery.

Historical backtests should run 04A then 04B before 04 so historical news rows have AI impact scores.
