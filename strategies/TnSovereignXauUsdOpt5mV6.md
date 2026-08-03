# TnSovereignXauUsdOpt5mV6 — TeleNexus 主權 XAU/USD 優化 5 分鐘策略

## 概述
移植自 `Paulaustin3977/OANDA-XAUUSD-Optimized-5m` 的 `OANDA_XAUUSD_Optimized_5m_Current.pine`。為**研究型（Paper/Strategy Tester only）**策略，參數凍結自 OANDA 60 天實務數據優化掃描，適用黃金（XAU/USD）5 分鐘圖。不連真實經紀商，不發送即時委託。

## 核心邏輯

### 訊號（EMA + BB 匯流）
- **EMA 9/18 交叉**：快線穿越慢線為基礎訊號
- **多頭確認**：`close > emaFast > emaSlow` 且 `close > BB 中線` 且 `RSI ∈ (45, 70)`
- **空頭確認**：`close < emaFast < emaSlow` 且 `close < BB 中線` 且 `RSI ∈ (30, 55)`

### 精選 UTC 時段
掃描選出的六個時段（UTC 02 / 08 / 15 / 18 / 19 / 21 時），僅在這些時段允許進場。

## 風險管理
- **ATR Bracket**：SL = 入場價 ∓ `ATR × 2.0`，TP = 入場價 ± `ATR × 2.5`
- **Max-Hold**：持有超過 3 根完整 5m K 線強制平倉
- **Cooldown**：每筆平倉後冷卻 1 根 K 線
- **僅當日內訊號可進場**：`barstate.isconfirmed` 與 `position_size == 0` 門檻

## 視覺
EMA 9/18、BB 中線、active stop/target（持倉時以 `plot.style_linebr` 顯示）、精選時段以青綠色背景標示。

## 版號
- 版本：v26.0803.1922
- 審計時間：2026-08-03 19:22 CST
- 來源：Paulaustin3977/OANDA-XAUUSD-Optimized-5m
