# 🛡️ TeleNexus Adaptive Vol Regime Sovereign (v26.0417.1500)

## 📌 策略概述
此策略是 TeleNexus 針對市場政權（Regime）切換的工業級實作。它利用 `ta.percentrank` 監測市場波動率在歷史區間中的百分位排名，從而動態決定目前應採用的執行邏輯（均值回歸或趨勢追蹤）。

## 🛠️ 主權化改進 (Sovereign Enhancements)
1. **v6 Enum 狀態機**：使用 Pine Script v6 原生 Enum 定義 `LowVol`, `MidVol`, `HighVol` 三種規訓狀態。
2. **跨資產基準過濾**：強制請求 `AMEX:SPY` 的日線 200 EMA 作為「主權安全」基準，杜絕在大盤崩潰時執行高風險操作。
3. **物理狀態標籤**：透過 v6 Table API 即時在圖表上顯示目前的波動率百分位排名與政權狀態。

## 📊 核心觀察
- **波動率對沖**：透過百分位排名而非固定數值，使策略能自適應不同資產的波動特性。
- **風險規訓**：在高波動（Crisis）狀態下，策略自動進入 Risk-Off 模式，僅保留極高信賴度的過濾進場。

## 🚀 執行指令
在 TradingView 加載 `adaptive_vol_regime_sovereign_v6.pine`，觀察背景顏色的切換（藍色為低波動，綠色為穩定趨勢，紅色為高風險）。
