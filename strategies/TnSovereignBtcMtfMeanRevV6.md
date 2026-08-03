# TnSovereignBtcMtfMeanRevV6 — TeleNexus 主權 BTC 多時框均值回歸策略

## 概述
移植自 `JusticeWiz/btc-mean-reversion-bot` 的 `strategy.pine`。為**超保守 BTC 均值回歸**策略：1 分鐘執行框架，搭配 5 分鐘多時框（MTF）過濾、波動壓縮、動態影線篩選與程式化風險管理護欄，配即時 UI 儀表板。

## 核心邏輯

### 入場（1m 極端 + 超保守門檻）
- **做多**：`close < BB 下軌(20, 2.5)` 且 `RSI(2) < 10` 且 `wickOK` 且 `atrFloor` 且 `ranging1m` 且 `mtfOK`
- **做空**：`close > BB 上軌` 且 `RSI(2) > 90` 且同組過濾
- **出場**：價格回到 BB 中線或 RSI 反轉（60/40）

### 多時框確認（MTF）
- **1m ADX** `< 20`：確保僅在區間市況進場
- **5m ADX** `< 20`：區間確認
- **5m RSI** ∈ (40, 60)：中性帶
- **5m EMA(50) 斜率** < 0.03%：平坦趨勢

### 額外過濾
- **影線篩選**：上下影線各佔 K 線範圍 < 35%
- **波動壓縮**：`ATR < SMA(ATR, 50)`
- **NY 時段**：僅 13:30–20:00 UTC
- **價差代理**：`high - low <= spreadThresh`

## 風險管理（程式化護欄）
- **每日虧損上限**：`dailyLossLimit` 觸及即 Kill-Switch
- **連續虧損上限**：`maxLossStreak` 強制停用
- **冷卻**：虧損後 1 次/2 次連虧分別冷卻 5/10 根
- **固定美元風險**：`qty = riskDollars / stopDist`
- **ATR Stop/Target**：SL = 0.5× ATR，TP = 0.25× ATR
- **JSON Alert**：entry/exit/kill 均輸出 JSON 供 Webhook 橋接

## 儀表板
右上角 8 行表：Regime、5m Trend、Spread、Session、Cooldown、Kill-Switch、MTF、當日交易統計。

## 版號
- 版本：v26.0803.1922
- 審計時間：2026-08-03 19:22 CST
- 來源：JusticeWiz/btc-mean-reversion-bot
