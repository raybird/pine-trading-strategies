# 📂 Strategies Catalog

這是 TeleNexus 旗下所有已實體化的 Pine Script v6 策略清單，按技術邏輯分類：

### 🏛️ Sovereign Core (主權核心系列)
- [`tn_sovereign_v6.pine`](./tn_sovereign_v6.md): 基礎主權交易框架。
- [`tn_universal_sovereign_v6.pine`](./tn_universal_sovereign_v6.md): 通用型主權規訓策略。
- [`tn_multi_audit_sovereign_v6.pine`](./tn_multi_audit_sovereign_v6.md): 多維因果審計主權系統。
- [`TnSovereignMtfIntradayV6.pine`](./TnSovereignMtfIntradayV6.md): 多時框因果對位日內策略。
- [`TnSovereignMtfViopV6.pine`](./TnSovereignMtfViopV6.md): 具備時序審計特徵的多時框 VIOP 策略。

### 📐 Market Structure & Price Action (市場結構與價格行為)
- [`ZzcMarketStructureSovereignV6.pine`](./ZzcMarketStructureSovereignV6.md): 波段結構主權策略 (ZZC)。
- [`XauusdIntradayTrendPullbackV6.pine`](./XauusdIntradayTrendPullbackV6.md): 黃金日內趨勢拉回策略。
- [`fvg_orderblock_sovereign_v6.pine`](./fvg_orderblock_sovereign_v6.md): 公允價值缺口與訂單塊對位。
- [`smc_sovereign_v6.pine`](./smc_sovereign_v6.md): 聰明錢概念 (SMC) 主權化實作。
- [`tn_sovereign_darvas_v6.pine`](./tn_sovereign_darvas_v6.md): 自動化達瓦斯箱體規訓。
- [`tn_sovereign_fibonacci_v6.pine`](./tn_sovereign_fibonacci_v6.md): 結構性斐波那契回撤系統。
- [`TnSovereignAdvancedSwingV6.pine`](./TnSovereignAdvancedSwingV6.md): 多維時序對位進階波段策略。
- [`ZzcCorridorSovereignV6.pine`](./ZzcCorridorSovereignV6.md): 整合擠壓偵測與 Wyckoff 審計的波段走廊主權策略。

### 📊 Volume & Order Flow (成交量與訂單流感知)
- [`volume_profile_matrix_v6.pine`](./volume_profile_matrix_v6.md): 自適應成交量分佈矩陣。
- [`tn_footprint_imbalance_v6.pine`](./tn_footprint_imbalance_v6.md): 足跡圖失衡偵測主權版。
- [`of_imbalance_matrix_map_v6.pine`](./of_imbalance_matrix_map_v6.md): 訂單流失衡矩陣地圖。
- [`footprint_entropy_sovereign_v6.pine`](./footprint_entropy_sovereign_v6.md): 訂單流熵值主權分析。
- [`footprint_explorer_v6.pine`](./footprint_explorer_v6.md): 實體買賣壓力感知。
- [`footprint_liquidity_sweep_v6.pine`](./footprint_liquidity_sweep_v6.md): 足跡圖流動性獵取。

### 🧮 Matrix & Machine Learning (矩陣與機器學習增強)
- [`matrix_knn_ml_v6.pine`](./matrix_knn_ml_v6.md): 基於矩陣的 KNN 鄰近演算法。
- [`ml_matrix_ensemble_v6.pine`](./ml_matrix_ensemble_v6.md): 機器學習矩陣集成系統。
- [`monte_carlo_risk_matrix_v6.pine`](./monte_carlo_risk_matrix_v6.md): 蒙地卡羅風險模擬矩陣。
- [`matrix_ols_stat_arb_v6.pine`](./matrix_ols_stat_arb_v6.md): 矩陣 OLS 統計套利。
- [`causal_matrix_weights_v6.pine`](./causal_matrix_weights_v6.md): 因果權重演算矩陣。

### 🐝 Multi-Agent & Swarm (多智能體與蜂群協作)
- [`federated_consensus_sovereign_v6.pine`](./federated_consensus_sovereign_v6.md): 聯邦共識主權投票系統。
- [`swarm_modular_executor_v6.pine`](./swarm_modular_executor_v6.md): 蜂群模組化執行器。
- [`multi_agent_of_ensemble_v6.pine`](./multi_agent_of_ensemble_v6.md): 多代理人集成訂單流。
- [`momentum_swarm_sovereign_v6.pine`](./momentum_swarm_sovereign_v6.md): 多資產動能輪動系統。

### 🌍 Macro & Optimization (宏觀建模與優化)
- [`macro_modeling_sovereign_v6.pine`](./macro_modeling_sovereign_v6.md): 宏觀環境狀態機規訓。
- [`yield_spread_sovereign_v6.pine`](./yield_spread_sovereign_v6.md): 美債收益率差主權監測。
- [`markowitz_portfolio_sovereign_v6.pine`](./markowitz_portfolio_sovereign_v6.md): 馬科維茨最小變異組合。
- [`tn_max_sharpe_sovereign_v6.pine`](./tn_max_sharpe_sovereign_v6.md): 最大夏普比率優化。

---
*註：所有的策略現在均具備 100% 的因果說明文件。*

### 🏛️ Sovereign FlowZone & Refinements (Batch 7)
- [`TnSovereignFlowZoneV6.pine`](./TnSovereignFlowZoneV6.md): 因果匯流主權策略。
- [`RsiMeanReversionSovereignV6.pine`](./RsiMeanReversionSovereignV6.md): 整合布林帶與 RSI 的均值回歸策略。
- [`TnSovereignFakeoutConfirmedV6.pine`](./TnSovereignFakeoutConfirmedV6.md): 具備四層過濾器的假突破確認主權策略。

- [`TnSovereignChandelierV6.pine`](./TnSovereignChandelierV6.md): 整合 200 EMA 與物理能量審計的吊燈止損趨勢策略。

- [`TnSovereignAdxTrendV6.pine`](./TnSovereignAdxTrendV6.md): 整合 ADX 趨勢強度審計與 ATR 風險對位的 v6 策略。

- [`TnSovereignMacdV6.pine`](./TnSovereignMacdV6.md): 整合動能斜率審計與 200 EMA 過濾的主權 MACD 策略。

- [`TnSovereignBbBreakoutV6.pine`](./TnSovereignBbBreakoutV6.md): 整合布林帶突破、肯特納擠壓與成交量審計的 v6 策略。

- [`TnSovereignSupertrendV6.pine`](./TnSovereignSupertrendV6.md): 整合多維趨勢地板 (200/50 EMA) 的主權超級趨勢策略。

- [`TnSovereignTripleEmaV6.pine`](./TnSovereignTripleEmaV6.md): 整合 5/13/34 對位與 200 EMA 全球地板的主權三均線策略。

- [`TnSovereignSessionQuantV6.pine`](./TnSovereignSessionQuantV6.md): 整合時段規訓與區間突破審計的 v6 策略。

- [`TnSovereignStochV6.pine`](./TnSovereignStochV6.md): 整合隨機指標區域審計與 200 EMA 過濾的主權反轉策略。

- [`TnSovereignFakeoutV6.pine`](./TnSovereignFakeoutV6.md): 整合四層物理過濾（量能、HTF、ATR）的主權防假突破策略。

- [`TnSovereignRsiAtrV6.pine`](./TnSovereignRsiAtrV6.md): 整合 RSI 動能門檻與 ATR 動態風險管理的主權 v6 策略。

- [`TnSovereignVolumeDeltaV6.pine`](./TnSovereignVolumeDeltaV6.md): 整合累積 Delta 背離偵測與 200 EMA 過濾的主權訂單流策略。

- [`TnSovereignSMCV6.pine`](./TnSovereignSMCV6.md): 整合流動性掃蕩與訂單塊確認的 v6 SMC 策略。
