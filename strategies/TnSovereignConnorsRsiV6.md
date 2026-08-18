# TnSovereignConnorsRsiV6 — TeleNexus Connors R2 短期均值回歸策略

## 概述
移植自 `Ahmed-GoCode/Quant-Edge-Indicators`（MPL-2.0）`RSI & Momentum/Larry Connors 2-Period RSI Strategy.pinescript`。以 **2-Period RSI (R2)** 捕捉短期極端情緒：R2 < 10 視為超賣耗竭買點，僅在高於長週期移動平均的趨勢環境中做多，R2 回升至 70 或持有滿 K 線數即獲利了結。Connors R2 對情緒反轉的反應遠快於傳統 14 期 RSI，在震盪市場具經典統計優勢。

## 核心邏輯
- **買點**：`R2 < buyThresh`（預設 10）且 `close > TrendMA`（SMA/EMA/RMA，預設 200）且無持倉
- **對偶短點**：`R2 > 100 - buyThresh` 且趨勢向下（Short 開關可獨立關閉）
- **出場**：`R2 > exitThresh`（預設 70）回升出場，或 Max-Bars-In-Trade（預設 3，原版參數）強制獲利了結
- **可選落地保護**：ATR Stop（關閉以忠於 Connors 原版僅以 RSI 情緒出場）
- **RVOL 過濾（可選）**：要求成交量相對移動平均爆量（>2.0）驗證情緒耗竭

## 風險管理
- 多/空獨立開關 + 測試窗時間過濾
- 原版不設 Stop（依賴 RSI 快閃出場）；本版提供 ATR 災難 Stop 選項
- 單一倉位（`pyramiding=0`），權益百分比倉位

## Sovereign Overlays
- R2 軌跡 + 買/賣閘門區填充 + 陰陽零軸視覺
- Webhook 就緒 `alertcondition`（買點/賣點/多單離場）
- HUD：R2 值、趨勢狀態、持倉 K 線數、版號（v26.0819.0630）

## 版號
- 版本：v26.0819.0630
- 審計時間：2026-08-19 06:30 CST
- 來源：Ahmed-GoCode/Quant-Edge-Indicators（MPL-2.0）