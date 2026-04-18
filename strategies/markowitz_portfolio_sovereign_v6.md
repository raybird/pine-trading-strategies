# TN Markowitz GMVP Sovereign v6 (馬科維茨最小變異組合版)

## 策略概述
此策略致力於解決多資產配置中的風險最小化問題。它在 Pine Script v6 中實作了現代投資組合理論 (MPT) 的核心——全球最小變異數組合 (Global Minimum Variance Portfolio)。透過矩陣代數動態求解資產間的協方差矩陣與最優權重，實現自動化的資產再平衡與系統性風險對沖。

## 核心特性
- **矩陣化協方差演算 (Covariance Engine)**: 全量利用 `matrix` 運算，動態計算多個資產（如 BTC, ETH, SOL）的收益率矩陣、去中心化處理及協方差矩陣。
- **動態權重優化 (Weight Optimization)**: 實裝了矩陣求逆 (`inv`) 與轉置 (`transpose`) 邏輯，自動求解滿足「變異數最小」約束的資產權重分布。
- **三級再平衡規訓 (Rebalance Frequencies)**:
  1. **Fast (10 Bars)**: 快速響應波動位移，適合震盪市。
  2. **Standard (20 Bars)**: 標準規訓頻率，平衡交易成本與風險。
  3. **Sovereign (50 Bars)**: 長週期主權配置，鎖定趨勢溢價。
- **權重視覺化儀表板**: 利用 Table API 即時披露各資產的 GMVP 權重係數，並根據權重強度動態渲染背景色彩。

## 使用建議
- **主週期**: 建議在 4H 或 Daily 週期使用。
- **資產選擇**: 建議選擇具備一定相關性但非完全同步的標的，以發揮 MPT 的分散風險效果。
- **版本號**: v26.0418.0715
