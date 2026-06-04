# tn_pair_corr_divergence_v6 — TeleNexus Pair Correlation Z-Score Divergence (Sovereign Port)

> **Version:** v26.0605.0630 | **CST:** 2026-06-05 06:30  
> **Origin:** [PineGen-AI/pair-correlation-divergence-strategy](https://github.com/PineGen-AI/pair-correlation-divergence-strategy)  
> **Category:** Multi-Agent, Swarm & Macro → Pair Correlation

## Concept

This strategy detects relative divergence between two correlated assets by computing the Z-score of their return spread. When the spread deviates beyond a threshold (one asset has outperformed the other significantly), the strategy bets on mean reversion of the spread, filtered by trend, momentum, and correlation strength.

## Core Logic

1. **Return Spread**: Computes ROC for both assets, spread = ret1 - ret2
2. **Z-Score Normalization**: `(spread - SMA(spread, 30)) / stdev(spread, 30)`
3. **Trend Filter**: Fast EMA > Slow EMA on primary asset → long bias
4. **Momentum Filter**: RSI > 50 + MACD line > signal line
5. **Correlation Filter**: Only trades when correlation ≥ 0.5 (configurable)
6. **Exit**: Z-score reverts toward zero, or ATR-based SL/TP

## Sovereign Enhancements

- Added `barstate.isconfirmed` for non-repainting signals
- Causal audit label on last bar (last signal, Z at entry, correlation)
- Exit zone lines on chart for visual confirmation
- Configurable R:R ratio separate from ATR stop
- Correlation filter toggle

## Parameters

| Parameter | Default | Description |
|-----------|---------|-------------|
| Primary Asset | OANDA:EURUSD | First pair leg |
| Secondary Asset | OANDA:GBPUSD | Second pair leg |
| Correlation Length | 50 | Lookback for correlation calc |
| Z-Score Length | 30 | Lookback for Z-score calc |
| Z Entry Threshold | 1.0 | Z-score to enter |
| Z Exit Threshold | 0.1 | Z-score to exit |
| ATR Length | 14 | Volatility reference |
| Risk:Reward | 2.0 | TP = ATR*1.5*RR |
| Fast/Slow EMA | 20/50 | Trend direction |
| RSI Length | 14 | Momentum filter |
| MACD | 12/26/9 | Momentum confirmation |
| Min Correlation | 0.5 | Correlation floor |
| Correlation Filter | true | Toggle correlation gate |

## Usage Notes

- Best on correlated pairs (EURUSD/GBPUSD, XAUUSD/XAGUSD, etc.)
- Z-Score entry threshold can be tuned per pair; 1.0–2.0 typical
- Correlation filter prevents trading in low-relationship regimes
- `overlay=false` — Z-score plotted in separate pane