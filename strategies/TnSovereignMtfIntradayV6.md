# Tn Sovereign MTF Intraday v6

## 策略概述
這是一款基於多時框 (MTF) 因果對位的日內主權交易策略。它透過高時框 (HTF) 捕捉市場結構與趨勢背景（結合 EMA 與 Supertrend），並在小時框捕捉局部動能與成交量匯流進場。此策略嚴格遵循 TeleNexus 的「非重繪 (Non-repainting)」與「物理對位」規訓。

## 核心特性
- **雙層趨勢過濾**: 結合 HTF EMA 與 Supertrend 進行背景判定，確保執行方向與大週期共振。
- **成交量放大規訓**: 僅在成交量突破均值 (SMA) 指定倍數時進場，過濾無效的低流動性波動。
- **自適應 ATR 風險管理**: 
  - 動態止損 (SL) 與獲利 (TP) 基於當前市場波動率。
  - 整合 ATR 噪聲過濾，避免在低波動盤整期頻繁止損。
- **物理時間對位**: 版本號與代碼內部標註嚴格對齊系統物理時間 (CST)，確保因果一致性。

## 模組說明
1. **Module 1 (Sovereign Inputs)**: 參數化管理，支持多時框設定與風險倍數調整。
2. **Module 2 (Data Acquisition)**: 使用 `request.security` 配合 `[1]` 偏移量獲取高時框數據，杜絕未來函數。
3. **Module 3 (Causal Signals)**: 整合趨勢、動能、成交量與噪聲四重過濾門檻。
4. **Module 4 (Execution)**: 執行 `strategy.entry` 與 `strategy.exit`。
5. **Module 5 (Visualization)**: 包含趨勢背景渲染與即時執行監控儀表板。

## 使用建議
- **推薦標的**: 指數 (ES, NQ)、黃金 (XAUUSD) 或高波動外匯。
- **時間週期**: 建議以 1M 為進場週框，5M 為趨勢週框。
- **版本號**: v26.0418.0600
