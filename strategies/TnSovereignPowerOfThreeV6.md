# TnSovereignPowerOfThreeV6 (v26.0618.1830)

> **「市場的每一步推進，都歷經 Accumulation → Manipulation → Distribution 的因果循環。」**

## 1. 核心精髓 (Essence)
本策略移植自 FEELS Power of Three v1.5，經 TeleNexus 主權框架重寫為完整交易策略。
核心邏輯為 POI (Power of Interest) 三相位循環偵測：**Accumulation（累積區間建構）→ Manipulation（流動性掠奪與陷阱確認）→ Distribution（方向性擴張）**。
不同於傳統 SMC 策略的靜態結構，PO3 引擎追蹤完整的相位狀態機，並輸出歷史頻率統計以提高決策透明度。

## 2. 三相位因果引擎 (Causal Phases)
- **Phase 0 (Accumulation)**: 價格在週期開盤價附近建構區間，等待外部流動性觸發。
- **Phase 1 (Manipulation)**: 價格突破累積區間掠奪止損，進入確認等待狀態。
- **Phase 2 (Trap Confirmed)**: 價格回到區間內確認陷阱，但尚未展開方向。
- **Phase 3 (Distribution)**: 價格穿越週期開盤價，方向性擴張正式啟動。

## 3. 主權過濾器 (Sovereign Filters)
- **HTF Bias**: Daily EMA 50 趨勢偏向對位（確保與大資金方向一致）。
- **Confluence Score (1-4)**: 相位有效 + HTF 對位 + 陷阱確認 + 分佈展開。
- **ATR 風控**: 動態 SL/TP 基於當前波動率。

## 4. 規訓記錄 (Audit Log)
- **v26.0618.1830**: 首版移植自 FEELS Power of Three v1.5。完整 Pine Script v6 實作，含 Dashboard 與 Alert。

---
*Calibrated at Thu Jun 18 18:30:05 CST 2026 | Calibration: Sovereign*
