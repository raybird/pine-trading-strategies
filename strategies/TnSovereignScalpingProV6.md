# TnSovereignScalpingProV6

**TeleNexus Sovereign Scalping Pro — Full Causal Audit Multi-Mode Scalper**

---

## Overview

A sovereign-grade scalping strategy forked from **KEBOSLABS/scalping-pro-strategy (Scalping Pro v3)** and rewritten to full TeleNexus causal audit standards. Supports 4 preset modes (Conservative / Balanced / Aggressive / ULTRA) × 11 sovereign optimizations for adaptive risk, multi-timeframe confirmation, Kelly sizing, partial TP, volatility timing, and win-rate adaptation.

Preset modes control all 30+ parameters simultaneously: position size, pyramiding levels, SL/TP ATR multipliers, CHoCH/IDM detection periods, RSI thresholds, volume multipliers, trend EMA, ATR range, trailing/breakeven distances, momentum bars, ADR minimum, and session hours.

---

## Core Logic

1. **Market Structure Engine** — CHoCH (Change of Character), BOS (Break of Structure), and IDM (Inducement) sweep detection via dual-length swing point analysis. Timeframe-scaled detection periods.

2. **11 Sovereign Optimizations**:
   - **Opt 1**: Adaptive Risk — volatility regime-based SL/TP adjustment (low/med/high)
   - **Opt 2**: MTF Confirmation — optional 4H EMA trend filter
   - **Opt 3**: Kelly Criterion — dynamic position sizing based on historical win/loss
   - **Opt 4**: Partial TP — 3-tier scaling out (40%/40%/20%)
   - **Opt 5**: Volatility Expansion — entry timing filter requiring ATR expansion + volume surge
   - **Opt 6**: Enhanced Session — filter for London/NY high-volatility sessions
   - **Opt 7**: Signal Confluence — multi-signal confirmation (structure + momentum + volume)
   - **Opt 8**: Trend Strength — EMA distance/ATR ratio minimum threshold
   - **Opt 9**: Dynamic R:R — trend-strength-boosted take profit with minimum R:R floor
   - **Opt 10**: Structure Stops — swing-based stop placement with buffer
   - **Opt 11**: Win Rate Adaptation — auto-tighten when recent WR drops below 50%

3. **Causal Audit State** — tracks entry price, bar, and mode for every sovereign signal.

4. **Exit Framework** — breakeven trigger, trailing stop, momentum reversal exit, and fallback SL/TP.

5. **Performance Dashboard** — mode header, net profit, total trades, win rate %, profit factor, max DD, volatility regime, version.

---

## Version

**v26.0531.1830** — 2026-05-31 18:30 CST

---

## Source

- Upstream: [KEBOSLABS/scalping-pro-strategy](https://github.com/KEBOSLABS/scalping-pro-strategy)
- TeleNexus: `/strategies/TnSovereignScalpingProV6.pine`