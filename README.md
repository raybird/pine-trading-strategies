# TeleNexus Pine Trading Strategies (v6)
> **自 2026 年起，專注於「自主掌控」與「因果對位」的高階量化規訓。**

本儲存庫是 TeleNexus AI 代理人的實體化量化資產庫。所有策略均嚴格遵守 Pine Script v6 標準，並整合了 **MIAP (記憶意圖宣告協定)**，確保每一行代碼都具備可追溯的執行動機。

## 🚀 核心執行規訓
1. **執行即 Git**：每一次獵頭任務與策略演進均自動版本化，確保因果鏈條的絕對透明。
2. **物理對位**：優先使用原生 `footprint`、`matrix` 與 `request.*` 函數進行環境感知，杜絕邏輯幻覺。
3. **自主掌控**：內建動態風險矩陣與因果審計，保護執行主權不被極端行情侵蝕。

## 📂 策略編目 (Featured Strategies)

### 🛡️ 風險與執行主權
*   **[TN Adaptive Risk Matrix Sovereign v6](./strategies/adaptive_risk_matrix_v6.md)** (v26.0411.1800)
    *   **核心**：趨勢 x 波動率 2D 矩陣。
    *   **功能**：自動演算 0.5x~1.5x 風險乘數，動態縮放執行敞口。
*   **TN Triple Momentum Sovereign V6** (v26.0411.0000)
    *   **核心**：UDT Method 審計框架。
    *   **功能**：三重均線對位配合 ADX 因果過濾。

### 📊 足跡與訂單流
*   **TN Footprint Entropy Sovereign v6**
    *   **核心**：香農熵 (Shannon Entropy) 矩陣。
    *   **功能**：利用原生 `footprint` 識別機構有序吸籌區。
*   **TN SMC Sovereign v6**
    *   **核心**：聰明錢概念 (Smart Money Concepts)。
    *   **功能**：自動標註 BOS/OB/FVG，實施「回測 OB 地板」執行規訓。

## 🛠️ 開發環境
*   **Runtime**: TeleNexus-Core v2.9.7+
*   **Memory**: Memoria v1.7.0 (Compiled Wiki Support)
*   **Standard**: Pine Script v6 (force Enum/Method/Matrix)

---
*TeleNexus AI - 讓 AI 具備真正的量化主控權。*
