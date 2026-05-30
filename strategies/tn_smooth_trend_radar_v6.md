# TeleNexus Sovereign Smooth Trend Radar V6

> **分類**: Trend & Momentum / Supertrend  
> **版號**: v26.0530.1831  
> **獵頭源**: WavesUnchained Smooth Trend Radar v3.3  
> **狀態**: 已實體化

---

## 策略概述

雙平滑 Supertrend 趨勢追蹤策略。核心創新為**WMA + EMA 雙重平滑 Baseline**，大幅減少 whip-saw，結合 pivot rejection 訊號過濾與多種 SL/TP 方法。

## TeleNexus Sovereign 強化

| 項目 | 原始 | 強化後 |
|------|------|--------|
| 基礎線 | WMA + EMA 雙平滑 | 加入 Auto Timeframe Scaling |
| 入場 | 翻轉 + rejection | Re-Entry After SL Hit 機制 |
| 風險管理 | 單一 SL/TP | Breakeven + Trailing + Multi-TP |
| 時框適應 | 手動參數 | 自動適配 1m ~ 1W |

## 核心邏輯

1. **Supertrend Midline** — (HL2 ± factor × ATR) 經 WMA → EMA 雙平滑
2. **Trend 方向** — Baseline 斜率: crossover → Bull, crossunder → Bear
3. **Rejection 偵測** — Pivot Low/High 觸及 Baseline + 斜率確認 + 觸碰計數
4. **Polarity Filter** — Body (收盤方向) 或 Pressure (收盤位置)
5. **Auto Timeframe Scaling** — 依 TF 自動選擇最佳參數

## 參數建議

| 參數 | 預設 | 說明 |
|------|------|------|
| Supertrend Factor | 12 | Baseline 寬度 |
| WMA Length | 40 | 第一層平滑 |
| EMA Length | 14 | 第二層平滑 |
| Min Baseline Touches | 2 | Rejection 門檻 |
| Stop Loss | 1.5 ATR | 風險管理 |
| Take Profit | 3.0 ATR | 止盈距離 |

## 風險

- 雙平滑在高 TF (4H+) 有較大 lag
- Rejection 在低波動時減少訊號頻率
- 適合趨勢市場，橫盤期應降低倉位