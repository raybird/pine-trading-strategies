# 🧲 TN Sovereign Liquidity Hunt v6

## 🚀 策略概述
`TN Sovereign Liquidity Hunt v6` 是一款專門用於識別「流動性獵殺 (Liquidity Sweep)」與「機構位移 (Institutional Displacement)」的進階交易策略。它基於 **Pine Script v6** 嚴格標準撰寫，旨在捕捉市場在突破關鍵高低點後產生的反向因果引力或強勢趨勢確認。

## 🧠 核心邏輯 (Causal Logic)
1.  **流動性池識別**：自動定標過去 N 根 K 線的物理邊界作為流動性池 (Liquidity Pools)。
2.  **獵殺特徵感應**：當價格影線 (Wick) 穿透流動性池但實體回縮，且影線比例符合規訓時，判定為流動性獵殺。
3.  **因果位移審計**：獵殺發生後若伴隨成交量放大，則確認為機構級別的位移信號。
4.  **v6 規訓實裝**：全面移除舊有的 `when` 參數，改用結構化的 `if` 條件塊，確保執行路徑的確定性。

## ⚙️ 輸入參數
- **Pivot Lookback**: 流動性池的回溯週期。
- **Wick-to-Body Ratio**: 判定獵殺行為的影線/實體比例。
- **Volume Displacement Mult**: 位移確認的成交量倍數。
- **Risk Architecture**: 基於 ATR 的主權動態風險配置。

## 📊 適用環境
- **適用周期**：5M, 15M, 1H (當沖與短線波段)。
- **適用標的**：BTC, 外匯主對, 納斯達克指數。

---
*Version: v26.0427.1830 | 專注於捕獲市場深層引力與機構足跡。*
