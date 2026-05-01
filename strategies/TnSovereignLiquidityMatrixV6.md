# TnSovereignLiquidityMatrixV6 (v26.0502.0830)

> **「市場不是隨機的波動，而是由高能量錨點支撐的物理矩陣。」**

## 1. 核心精髓 (Essence)
本策略繼承自 `h33rnan` 的 Adaptive Liquidity Matrix 研究，並將其算理與 TeleNexus 的「機構因果」規訓融合。它透過在宏觀週期（如日線）中尋找最高成交量的 K 線作為物理錨點（Anchor），並以此為中心利用 ATR 斐波那契擴展生成動態流動性矩陣帶。

## 2. 矩陣規訓矩陣 (Matrix Regulation)
- **宏觀錨定 (Macro Anchoring)**: 自動檢索指定回溯窗格內的成交量巅峰，對位機構真實入場意圖。
- **動態擴展 (Adaptive Expansion)**: 使用 MTF ATR 作為矩陣帶寬與間距的驅動因子，確保矩陣能自動適應當前市場的波動密度。
- **緩和效應審計 (Mitigation Audit)**：自動識別已被價格穿透的「鬼魂區域 (Ghost Zones)」並降低其因果權重。
- **量能確認 (Volume Confirmation)**：僅當價格在矩陣帶內產生「共振」且伴隨 1.5 倍以上的量能突發時，才視為有效的因果信號。

## 3. 性能指標 (Expected Performance)
- **環境**: 1H / 4H 高波動資產（如 BTC, Gold）。
- **特徵**: 捕捉結構性反轉與突破回測。
- **止損**: 物理錨點對位止損，具備極強的生存能力。

## 4. 規訓記錄 (Audit Log)
- **v26.0502.0830**: 首版實體化。將「流動性矩陣」指標重構為全自動化策略，實裝了物理錨點追蹤與因果密度日誌。

---
*Calibrated at Sat May 2 08:30:20 CST 2026 | Calibration: Sovereign*
