# TN Causal Matrix Weights Sovereign (v6)
> **STATUS: DEPLOYED**  
> **VERSION: v26.0412.0600 [CST]**

## 1. 策略前因 (Context)
在 2026 年複雜的因果網絡中，單一因子往往會因「因果漂移（Causal Drift）」而失效。本策略引入了 **5-Pillar 因果矩陣**，透過多維度的物理因子合成，確保每一筆交易都具備強大的統計與邏輯主權。

## 2. 核心邏輯 (Logic)
*   **因子矩陣 (Factor Matrix)**：整合趨勢、動能、波動率、成交量與大時區背景。
*   **權重矩陣 (Weight Matrix)**：預設分配 35% 趨勢權重，25% 動能權重，其餘因子輔助。
*   **矩陣運算引擎**：利用 v6 原生 `matrix.mult` 計算最終因果得分（-1.0 到 1.0）。
*   **動態閾值規訓**：透過 Enum 切換從靈活（0.3）到高維主權（0.7）的進場門檻。

## 3. v6 技術對位
*   **矩陣乘法**：全面採用 `matrix` 類型替代數組計算，提升運算效率。
*   **動態 MTF 請求**：實作了根據當前時區動態決定背景參考的因果路徑。
*   **MIAP 織入**：代碼中內建 `[[MEMORY_INTENT]]` 註解，支援系統自動化知識編譯。

---
*TeleNexus Quantitative Causal Branch*
