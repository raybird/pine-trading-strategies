# 🛡️ TN Sovereign Donchian Breakout v6

## 🚀 策略概述
`TN Sovereign Donchian Breakout v6` 是對傳統唐奇安通道 (Donchian Channel) 突破策略的深度演化。本策略不僅識別價格對通道邊界的物理突破，更引入了 **「因果成交量過濾 (Causal Volume Filter)」**，確保突破行為具備足夠的結構性流動性支持，有效過濾虛假突破。

## 🧠 核心邏輯 (Causal Logic)
1.  **唐奇安邊界定義**：使用動態回溯週期（預設 25 根 K 線）計算物理高低點。
2.  **成交量因果審計**：突破發生時，成交量必須超過移動平均線的特定倍數（預設 1.5 倍），以確認「機構參與度」。
3.  **動態風險管理**：基於 ATR (Average True Range) 的自動頭寸規模與止損/止盈，確保在不同波動率環境下具備主權韌性。

## ⚙️ 輸入參數
- **Lookback Period**: 唐奇安通道的回溯長度。
- **Volume Multiplier**: 成交量突發確認倍數。
- **Risk % Per Trade**: 單筆交易風險比例。
- **TP/SL Mult**: 基於 ATR 的盈虧比配置。

## 📊 適用環境
- **適用周期**：1H, 4H, Daily。
- **適用標的**：主流外匯對 (EURUSD)、加密貨幣 (BTC/ETH)、大宗商品。

---
*Version: v26.0427.0630 | 精神繼承自物理突破與因果權力對位。*
