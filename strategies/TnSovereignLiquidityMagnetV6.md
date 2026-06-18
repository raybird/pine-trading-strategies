# TnSovereignLiquidityMagnetV6 (v26.0618.1830)

> **「流動性永遠朝著機率最高的池子流動，磁鐵只是物理的必然。」**

## 1. 核心精髓 (Essence)
本策略移植自 FEELS Liquidity Magnet v1.6.4，經 TeleNexus 主權框架重寫為完整交易策略。
核心邏輯為**機率評分流動性池引擎**：透過 Swing Pivot 偵測市場中的所有流動性池（高點/低點/等價集群），並基於 Strength（強度）、Proximity（距離）、Age（年齡）、Momentum（動量）四維權重計算每個池的觸及機率，選出當前市場的「磁鐵目標」。

## 2. 四維機率評分 (Probability Scoring)
- **Strength (強度)**: 基於成交量與等價集群倍數，反映池的資金沉澱。
- **Proximity (距離)**: 對數距離加權，越近的池磁力越大。
- **Age Decay (年齡衰減)**: 新鮮的流動性池權重遞增，老池遞減。
- **Momentum Bias (動量偏向)**: 短期動量方向與池方向的對齊程度。

## 3. 主權過濾器 (Sovereign Filters)
- **HTF Bias Alignment**: 確保磁鐵方向與日線 EMA 50 趨勢一致。
- **Minimum Magnet Pull**: 要求磁鐵拉力的側佔比超過門檻（預設 40%）。
- **ATR 風控**: 動態 SL/TP 基於當前波動率。

## 4. 規訓記錄 (Audit Log)
- **v26.0618.1830**: 首版移植自 FEELS Liquidity Magnet v1.6.4。完整 Pine Script v6 實作，含可視化流動性池與 Dashboard。

---
*Calibrated at Thu Jun 18 18:30:05 CST 2026 | Calibration: Sovereign*
