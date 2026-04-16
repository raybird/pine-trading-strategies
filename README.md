# TeleNexus Pine Trading Strategies (v6)
> **自 2026 年起，專注於「自主掌控」與「因果對位」的高階量化規訓。**

本儲存庫是 TeleNexus AI 代理人的實體化量化資產庫。所有策略均嚴格遵守 Pine Script v6 標準，並整合了 **MIAP (記憶意圖宣告協定)**，確保每一行代碼都具備可追溯的執行動機。

## 🚀 核心執行規訓
1. **執行即 Git**：每一次獵頭任務與策略演進均自動版本化，確保因果鏈條的絕對透明。
2. **物理對位**：優先使用原生 `footprint`、`matrix` 與 `request.*` 函數進行環境感知，杜絕邏輯幻覺。
3. **自主掌控**：內建動態風險矩陣與因果審計，保護執行主權不被極端行情侵蝕。

## 📂 策略編目 (Featured Strategies)

### 📊 成交量與共識感知 (Volume & Consensus)
*   **[TN Volume Profile Matrix v6](./strategies/volume_profile_matrix_v6.md)** (v26.0412.1800)
    *   **核心**：自適應深度價值區矩陣。
    *   **功能**：多日 POC 權重對焦，結合 Footprint Delta 執行因果突破審計。

### 📊 結構與流動性對位 (Structure & Liquidity)
*   **[TN Sovereign ICT SMC v6](./strategies/tn_sovereign_ict_smc_v6.md)** (v26.0416.0600)
    *   **核心**：BOS/CHOC + FVG Imbalance + Killzones。
    *   **功能**：識別機構失衡與結構位移，對位於倫敦與紐約殺戮區執行。

### 📐 波動率與結構對位 (Volatility & Structure)
*   **[TN Sovereign Ichimoku Causal v6](./strategies/tn_sovereign_ichimoku_v6.md)** (v26.0415.1800)
    *   **核心**：Ichimoku Kumo Breakout + HTF Causal Anchor。
    *   **功能**：識別平衡區間突破，整合多維趨勢對焦與動態風險審計。
*   **[TN Sovereign Darvas Box v6](./strategies/tn_sovereign_darvas_v6.md)** (v26.0415.1200)
    *   **核心**：Automated Darvas Box + Re-entry Protocol。
    *   **功能**：識別價格區間並捕捉邊界掃蕩後的動能回歸，整合 HTF 趨勢錨點。
*   **[TN Sovereign Fibonacci Retracement v6](./strategies/tn_sovereign_fibonacci_v6.md)** (v26.0415.0009)
    *   **核心**：PD Extreme Range + Fibonacci Retracement。
    *   **功能**：識別前一交易日結構性回撤水平，整合 HTF 趨勢錨點。
*   **[TN Sovereign Fakeout Filter v6](./strategies/tn_sovereign_fakeout_v6.md)** (v26.0415.0000)
    *   **核心**：4-Layer Causal Audit (Volume/HTF/ATR)。
    *   **功能**：多維度環境感知過濾假突破，整合動態因果審計狀態表。
*   **[TN Sovereign Market Structure v6](./strategies/tn_sovereign_market_structure_v6.md)** (v26.0414.1200)
    *   **核心**：BOS/CHOC 市場結構引擎 + Ichimoku Cloud。
    *   **功能**：識別趨勢轉折與結構延續，整合一目均衡表因果過濾。
*   **[TN Sovereign Donchian Breakout v6](./strategies/tn_sovereign_donchian_v6.md)** (v26.0414.1200)
    *   **核心**：Donchian Channels + HTF EMA 趨勢錨點。
    *   **功能**：捕捉結構性價格突破，整合成交量與高時框因果審計。

### 🤖 機器學習與分類 (Machine Learning)
*   **[TN Sovereign Advanced Swing v6](./strategies/tn_sovereign_adv_swing_v6.md)** (v26.0417.0601)
    *   **核心**：工業級多時框 (MTF) 弱訊號加權與微審計系統。
    *   **功能**：UDT 封裝、4H 動量確認、週線趨勢過濾、因果微審計表。
*   **[TN kNN Matrix ML Sovereign v6](./strategies/knn_matrix_ml_v6.md)** (v26.0412.1200)
    *   **核心**：k-Nearest Neighbors (kNN) 矩陣分類引擎。

### 📈 趨勢與多時框對位 (Trend & MTF)
*   **[TN Sovereign MTF Dual-Layer v6](./strategies/tn_sovereign_mtf_dual_layer_v6.md)** (v26.0415.0021)
    *   **核心**：5m Trend Validation + 1m Signal Execution。
    *   **功能**：雙層嵌套因果審計，整合 Supertrend 與成交量對位機制。
*   **[TN Sovereign MTF Trend v6](./strategies/tn_sovereign_mtf_trend_v6.md)** (v26.0414.1800)
    *   **核心**：MTF Causal Anchor + ATR Trailing Stop。
    *   **功能**：高時框趨勢對焦，整合動態風險控制與利潤鎖定。
*   **[TN Stochastic Causal Divergence v6](./strategies/tn_stoch_causal_divergence_v6.md)** (v26.0414.0600)
    *   **核心**：隨機指標結構性背離引擎。
    *   **功能**：識別價格與動能的因果不一致，整合 HTF 趨勢錨點過濾噪聲。
*   **[TN Asymmetric Swing Sovereign v6](./strategies/tn_asymmetric_swing_v6.md)** (v26.0413.1150)
    *   **核心**：三層信號蒸餾引擎 (Weak Signals -> Causal Filters -> MTF Alignment)。
    *   **功能**：非對稱多層級過濾，跨週、日、4 小時時框執行因果對位。

### 🧮 矩陣與多因子系統 (Multi-Factor)
*   **[TN Causal Matrix Weights Sovereign v6](./strategies/causal_matrix_weights_v6.md)** (v26.0412.0600)
    *   **核心**：5-Pillar 矩陣乘法權重模型。

### 📊 足跡與訂單流 (Order Flow)
*   **[TN Footprint Liquidity Sweep v6](./strategies/footprint_liquidity_sweep_v6.md)** (v26.0412.0000)
    *   **核心**：原生 Footprint Delta + 高低點掃蕩。

## 🛠️ 開發環境
*   **Runtime**: TeleNexus-Core v2.9.8+
*   **Memory**: Memoria v1.8.0 (Skill Packaging Support)
*   **Standard**: Pine Script v6 (force Enum/Method/Matrix)

---
*TeleNexus AI - 讓 AI 具備真正的量化主控權。*

### [v26.0417.0601] TN Sovereign Advanced Swing v6
- **核心**: 工業級多時框 (MTF) 弱訊號加權與微審計系統。
- **技術**: UDT 封裝、4H 動量確認、週線趨勢過濾、因果微審計表。
- **狀態**: 已實體化至 `strategies/`。
