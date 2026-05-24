# TnSovereignAdaptiveRegimeV6 — Adaptive Risk Regime Sovereign Strategy

**Version:** v26.0525.0630  
**Classification:** Volatility & Breakout / Multi-Agent  
**Author:** TeleNexus Studio (via PineGen-AI headhunt fusion)

---

## Overview

融合 PineGen-AI 三個前沿策略的核心邏輯，經 TeleNexus Sovereign 規訓重塑的單一主權策略：

1. **Adaptive Risk Regime** — ATR 波動率狀態切換（低波動均值回歸 / 高波動突破）
2. **Range Compression Expansion** — 壓縮區偵測 + 結構性突破
3. **Volatility Expansion Fake Breakout** — 假突破過濾（實體 K 線強度）

---

## Core Logic

### 1. Trend Regime (200 EMA Causal Floor)
- `emaBull = src > ema200` → 只做多
- `emaBear = src < ema200` → 只做空
- 200 EMA 作為因果趨勢地板，禁止逆勢交易

### 2. Volatility Regime Switching
- **Low Volatility (ATR < SMA-ATR)** → 均值回歸模式：從 range 邊界反轉交易
- **High Volatility (ATR > 1.3x SMA-ATR)** → 突破模式：跟隨動能方向
- **Compression (ATR < 0.7x SMA-ATR)** → 累積模式：等待壓縮釋放突破

### 3. Range Structure
- `rangeHigh = ta.highest(high, 20)` — 近期阻力
- `rangeLow = ta.lowest(low, 20)` — 近期支撐

### 4. Fake Breakout Filter
- 多頭：`close > open` (實體陽) 且 `close > high[1]` (突破前高)
- 空頭：`close < open` (實體陰) 且 `close < low[1]` (跌破前低)

### 5. Entry Conditions
| Regime | Bullish | Bearish |
|--------|---------|---------|
| Low Vol (Mean Rev) | `close < rangeLow[1]` (超賣反彈) | `close > rangeHigh[1]` (超買回落) |
| High Vol (Breakout) | crossUp + strongBull | crossDown + strongBear |
| Compression | crossUp + strongBull | crossDown + strongBear |

### 6. Risk Management
- SL: 1.5x ATR
- TP: 3.0x ATR
- 僅在無持倉時進場

---

## Parameters

| Param | Default | Description |
|-------|---------|-------------|
| ATR Length | 14 | ATR 計算週期 |
| Volatility Lookback | 50 | ATR 均線參考長度 |
| Compression Threshold | 0.7 | 壓縮判定倍率 |
| Expansion Multiplier | 1.3 | 擴張判定倍率 |
| Range Length | 20 | 高低點回溯長度 |
| SL ATR Multiplier | 1.5 | 止損倍率 |
| TP ATR Multiplier | 3.0 | 止盈倍率 |

---

## Signal Quality

| Mode | Expected Frequency | Best Market |
|------|-------------------|-------------|
| Mean Reversion | Medium (range-bound) | Sideways / Choppy |
| Expansion Breakout | Low (strong trends) | Trending / Momentum |
| Compression Accum | Low (before breakouts) | Consolidation → Expansion |

---

## HUD Dashboard

右上角 Sovereign Audit 面板顯示：
- Regime (Bull/Bear)
- Vol Regime (High/Compressed/Normal)
- ATR Ratio
- Range Width
- Current Mode
- SL/TP 數值
- Signal Status

---

## Notes

- 此策略為 PineGen-AI 三個策略的 Sovereign 融合版本，非原始複製
- 融合後的因果審計層（200 EMA）大幅降低假信號
- 不建議與 `TnSovereignMultiCausalityV6` 同時在同資金使用（因果疊加）