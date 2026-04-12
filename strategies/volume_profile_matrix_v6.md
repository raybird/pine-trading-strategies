# TN Volume Profile Adaptive Matrix (v6)
> **STATUS: DEPLOYED**  
> **VERSION: v26.0412.1800 [CST]**

## 1. 策略前因 (Context)
在 2026 年的高頻博弈環境中，單日價值區往往具備較大的偶然性。本策略旨在透過 **v6 矩陣架構** 維護多日價值區歷史，演算出市場真正的「共識中心 (Consensus Zone)」，並結合 Footprint 原生數據進行因果驗證，確保每一次突破都具備物理量能的支撐。

## 2. 核心邏輯 (Logic)
*   **自適應深度矩陣**：根據當前波動率 (ATR) 自動調整歷史價值區的權重深度。波動率高時矩陣收縮，追求即時性；波動率低時矩陣擴張，追求結構性。
*   **物理共識中心**：計算歷史 POC 的矩陣平均值，作為判斷趨勢強度的硬性地板。
*   **Delta 因果對位**：突破價值區邊界（VAH/VAL）時，強制要求 **Footprint Delta** 的方向與突破一致，杜絕虛假流動性陷阱。

## 3. v6 技術對位
*   **`request.footprint()`**：全面整合 v6 原生成交量分佈對象，實現了亞秒級的價值區數據獲取。
*   **`matrix.shift_rows`**：實作了高效的滾動數據管理，極大化了策略的運算主權。
*   **MIAP 織入**：內建 `[[MEMORY_INTENT]]` 標籤，支援系統將此策略自動歸類為「結構化共識審計」技能。

---
*TeleNexus Quantitative Causal Branch*
