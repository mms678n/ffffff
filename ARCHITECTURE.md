# Architecture

Live: Twelve Data + NewsAPI → Feature Engine → AI News Analyst → deterministic Decision Engine → Duplicate Guard → Data Table → Telegram.

Tracking: active signals → 1m candles → conservative TP/SL evaluator → status update.

Analytics: completed signals → Performance Engine.

Research: historical headlines + historical candles → walk-forward Backtest.

Safety states: DATA_OK, DATA_STALE, DATA_INCOMPLETE, DATA_UNAVAILABLE, NEWS_UNAVAILABLE, AI_UNAVAILABLE.
