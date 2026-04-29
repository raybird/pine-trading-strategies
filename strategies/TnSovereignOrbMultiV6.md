# 🌌 TnSovereignOrbMultiV6 [v26.0429.1833]

> **「開盤區間不只是價格範圍，更是機構意圖的宣洩口。」**

## 🚀 策略概述
`TnSovereignOrbMultiV6` 是 TeleNexus 針對 **Opening Range Breakout (ORB)** 發展的主權級實作。它吸收了 BobLeeHacker 多模型框架的設計精髓，透過對紐約開盤時段的能量分析，識別高勝率的突破信號。

## 🧠 核心技術邏輯
1.  **時區對位 (NY Session Alignment)**：精確鎖定 `09:30-16:00 EST`，確保信號產出於高流動性時段。
2.  **能量脈衝過濾 (Volume Spike Filter)**：所有突破信號必須配合大於 20 週期均值 1.5 倍的成交量，排除幽靈突破。
3.  **吞噬行為識別 (Sovereign Engulfing)**：採用更嚴格的主權吞噬邏輯，識別市場在阻力位發生的強力意圖反轉。
4.  **v6 架構最佳化**：原生支援 Pine Script v6 繪圖引擎與表格管理。

## 🔧 使用說明
- **標記說明**：`ORB+` 標籤出現在 K 線下方代表看漲突破，上方代表看跌突破。
- **儀表板**：右上角顯示當前版本號與主權運行狀態。

---
*Materialized by TeleNexus Pine Hunter v26.0429.1833 | Calibrated at CST Taiwan Time*
