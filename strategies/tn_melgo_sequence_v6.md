# TeleNexus Sovereign — Melgo Sequence v6

| Metadata | Value |
|----------|-------|
| **Version** | v26.0531.0630 |
| **Type** | Strategy |
| **Pine Script** | v6 |
| **Build** | 2026-05-31 06:30 (CST) |
| **Source** | Port of Melgo Sequence by Jeff Rey Melgo (@JeffMelgo) — ssrn.com/abstract=6658238 |

## Six-State Classification System

The Melgo Sequence classifies price action into six discrete market states using multi-source price synthesis (NA=HL2, SC=HLC3, FOT=OHLC4) combined with momentum, deviation, and volume-weighted analysis:

| State | Description | Favorability |
|-------|-------------|--------------|
| **Bull Trend** | Strong uptrend with confirmed momentum, not overextended | Long |
| **Bear Trend** | Strong downtrend with confirmed momentum, not overextended | Short |
| **Bull Rejection** | Uptrend structure but momentum fading and price overextended — potential reversal down | Long (counter-trend entry) |
| **Bear Indecision** | Downtrend structure but momentum recovering and price oversold — potential reversal up | Short (counter-trend entry) |
| **Distribution** | Upward structure with overextension and negative volume-weighted deviation — smart money distributing | Short |
| **Accumulation** | Downward structure with overextension and positive volume-weighted deviation — smart money accumulating | Long |

Neutral state is returned when no clear classification matches.

## Signal Logic

Entries are generated via multi-timeframe consensus voting:

1. **State Classification** is computed independently on 4 timeframes: 4H (Macro), 1H (Bias), 15M (Micro), 1D (Context)
2. **Consensus**: LONG requires 2+ TFs showing Bull Trend, Accumulation, or Bull Rejection; SHORT requires 2+ TFs showing Bear Trend, Distribution, or Bear Indecision
3. **Spread Filter**: Entry only fires when the 14-bar price range (as a multiple of ATR) exceeds 2.0
4. **Current TF Confluence**: The entry bar's own state must also match the trade direction

## Risk Management

| Parameter | Value |
|-----------|-------|
| Stop-Loss | 1.5× ATR from entry |
| Take-Profit | 3.0× ATR from entry |
| Position Sizing | Percent of equity (default 100%) |
| Cooldown | 3 bars after exit before re-entry |
| Direction Filter | Both / Long Only / Short Only |

## Recommended Timeframes

| Role | Timeframe | Purpose |
|------|-----------|---------|
| **Macro** | 4H | Primary trend direction and state |
| **Bias** | 1H | Intermediate bias and entry timing |
| **Micro** | 15m | Short-term state confirmation |
| **Context** | 1D | Higher-level regime filter |

The strategy should be applied on the **1H chart** with `request.security` fetching the other three timeframes internally.

## Attribution

Port of Melgo Sequence by **Jeff Rey Melgo** (@JeffMelgo)
Working paper: [ssrn.com/abstract=6658238](https://ssrn.com/abstract=6658238)