# Strategies Catalog

TeleNexus 旗下所有已實體化的 Pine Script v6 策略，按技術邏輯分類（共 121 個策略 + 1 核心庫）。

---

## Sovereign Core（主權核心，10）

| 策略 | 說明 |
|------|------|
| `tn_sovereign_v6` | 基礎主權交易框架 |
| `tn_universal_sovereign_v6` | 通用型主權規訓策略 |
| `tn_multi_audit_sovereign_v6` | 多維因果審計主權系統 |
| `TnSovereignMtfViopV6` | MTF VIOP，時序審計特徵 |
| `TnSovereignMtfIntradayV6` | 多時框因果對位日內策略 |
| `tn_sovereign_mtf_dual_layer_v6` | 雙層 MTF 主權策略 |
| `tn_sovereign_mtf_trend_v6` | MTF 趨勢主權策略 |
| `tn_sovereign_audit_v6` | 因果審計主權系統 |
| `tn_multi_factor_sovereign_v6` | 多因子主權策略 |
| `tn_session_sovereign_v6` | 時段規訓主權策略 |

## Trend & Momentum（趨勢與動量，12）

| 策略 | 說明 |
|------|------|
| `TnSovereignTripleEmaV6` | 5/13/34 EMA 對位 + 200 EMA 全球地板 |
| `TnSovereignMacdV6` | MACD + 動能斜率審計 + 200 EMA 過濾 |
| `TnSovereignHMAV6` | 雙重 HMA 對位 + 成交量能量審計 |
| `TnSovereignVortexV6` | 渦流極性審計 + 200 EMA 過濾 |
| `TnSovereignAdxTrendV6` | ADX 趨勢強度審計 + ATR 風險對位 |
| `TnSovereignSupertrendV6` | 多維趨勢地板 (200/50 EMA) 超級趨勢 |
| `TnSovereignSupertrendVolV6` | Supertrend ATR + 成交量放大確認 |
| `tn_triple_momentum_sovereign_v6` | 三重動量主權策略 |
| `TnSovereignOptimizedTrendV6` | 多尺度 EMA 交叉 + 成交量因果過濾 |
| `MtfTrendSovereignV6` | 多時框趨勢主權 |
| `tn_sovereign_vamo_v6` | VAMO 波動調整動量振盪器 |
| `TnSovereignVAMOStrategyV6` | VAMO 波動調整動量策略（完整版） |

## Mean Reversion & Oscillator（均值回歸與振盪指標，10）

| 策略 | 說明 |
|------|------|
| `TnSovereignStochV6` | 隨機指標區域審計 + 200 EMA 過濾 |
| `TnSovereignRsiAtrV6` | RSI 動能門檻 + ATR 動態風險管理 |
| `TnSovereignCCIV6` | 雙重 CCI 對位 + 200 EMA 趨勢地板 |
| `TnSovereignCMOV6` | CMO 動能背離 + 極端區域審計 |
| `TnSovereignFisherV6` | 費雪轉換極性審計 + 200 EMA 過濾 |
| `TnSovereignSTCV6` | 謝夫趨勢週期 + 200 EMA 過濾 |
| `TnSovereignVWAPV6` | 動態錨定 VWAP + 標準差通道均值回歸 |
| `TnSovereignVwapRegimeV6` | VWAP Regime 偏差策略 |
| `TnSovereignWaveTrendV20` | WaveTrend 熱力學反轉 |
| `RsiMeanReversionSovereignV6` | Bollinger + RSI 均值回歸 |

## Volatility & Breakout（波動率與突破，14）

| 策略 | 說明 |
|------|------|
| `TnSovereignAdaptiveRegimeV6` | ATR 波動率狀態切換 + 壓縮擴張 + 假突破過濾（PineGen-AI 融合） |
| `TnSovereignBbBreakoutV6` | Bollinger 突破 + Keltner 擠壓 + 成交量審計 |
| `TnSovereignKeltnerV6` | Keltner 通道突破 + ADX 動能過濾 |
| `TnSovereignChandelierV6` | Chandelier 止損 + 200 EMA 趨勢 |
| `TnSovereignDonchianV6` | 唐奇安通道突破 + 時序執行規訓 |
| `tn_sovereign_donchian_v6` | 成交量驗證 Donchian 突破 |
| `TnSovereignThermodynamicSqueezeV20` | 熱力學擠壓膨脹策略 |
| `TnSovereignThermodynamicBreakoutV20` | 熱力學膨脹突破策略 |
| `tn_compression_expansion_v6` | ATR 壓縮 → 膨脹突破 |
| `TnSovereignBreakoutConfluenceV6` | 突破共鳴策略 |
| `TnSovereignVolumeProfileScalpV6` | Volume Profile 精準 scalp |
| `TnSovereignOrbMultiV6` | 多模型 ORB 開盤區間突破 |
| `tokyo_breakout_v6_refined` | 東京時段突破策略 |
| `tn_asymmetric_swing_v6` | 不對稱波段策略 |

## Market Structure & Price Action（市場結構與價格行為，15）

| 策略 | 說明 |
|------|------|
| `ZzcMarketStructureSovereignV6` | ZZC 波段結構主權策略 |
| `ZzcCorridorSovereignV6` | 擠壓偵測 + Wyckoff 審計波段走廊 |
| `TnSovereignAdvancedSwingV6` | 多維時序對位進階波段 |
| `AdvancedSwingStrategyV6` | 進階波段策略（精簡版） |
| `tn_sovereign_adv_swing_v6` | 主權進階波段 |
| `TnSovereignMarketStructureV20` | 市場結構 + 熱力學策略 |
| `tn_sovereign_market_structure_v6` | 市場結構主權策略 |
| `tn_sovereign_fibonacci_v6` | 結構性 Fibonacci 回撤系統 |
| `tn_sovereign_darvas_v6` | 自動化 Darvas 箱體規訓 |
| `tn_sovereign_ichimoku_v6` | Ichimoku 主權策略 |
| `XauusdIntradayTrendPullbackV6` | 黃金日內趨勢拉回 |
| `smc_sovereign_v6` | 聰明錢概念 (SMC) 主權化 |
| `smc_matrix_sovereign_v6` | SMC 矩陣主權策略 |
| `fvg_orderblock_sovereign_v6` | FVG + 訂單塊對位 |
| `tn_sovereign_ict_smc_v6` | ICT/SMC 融合主權策略 |

### ICT / SMC 專項（跨類別，以上已計入）

| 策略 | 分類 |
|------|------|
| `TnSovereignIctV6` | ICT 2022 導師模型 |
| `TnSovereignIctSurgicalV20` | ICT 外科 + 熱力學 |
| `TnSovereignIctComboV6` | ICT 7 因子匯流 |
| `TnSovereignIctSmcComboV6` | ICT/SMC 7 因子匯流 |
| `TnSovereignSMCV6` | 流動性掃蕩 + 訂單塊確認 |
| `smc_sovereign_v6` | SMC 主權化 |
| `smc_matrix_sovereign_v6` | SMC 矩陣 |
| `fvg_orderblock_sovereign_v6` | FVG + 訂單塊 |
| `tn_sovereign_ict_smc_v6` | ICT/SMC 融合 |
| `TnSovereignFakeoutV6` | 四層防假突破 |
| `TnSovereignFakeoutConfirmedV6` | 四層過濾假突破確認 |
| `TnSovereignFakeoutFilterV6` | 四層因果審計假突破過濾 |
| `tn_fakeout_sovereign_v6` | 假突破主權策略 |
| `tn_fakeout_filter_v6` | 假突破過濾 |
| `tn_liquidity_sovereign_v6` | 流動性主權策略 |
| `TnSovereignLiquidityHuntV6` | 流動性獵殺 + 機構位移審計 |

## Volume & Order Flow（成交量與訂單流，11）

| 策略 | 說明 |
|------|------|
| `TnSovereignVolumeDeltaV6` | 累積 Delta 背離偵測 + 200 EMA 過濾 |
| `TnSovereignFootprintPOCV6` | 足跡圖 POC 突破 + 機構意圖審計 |
| `tn_footprint_imbalance_v6` | 足跡圖失衡偵測 |
| `footprint_explorer_v6` | 實體買賣壓力感知 |
| `footprint_liquidity_sweep_v6` | 足跡圖流動性獵取 |
| `footprint_entropy_sovereign_v6` | 訂單流熵值分析 |
| `of_imbalance_matrix_map_v6` | 訂單流失衡矩陣地圖 |
| `stacked_imbalance_sovereign_v6` | 堆疊失衡主權策略 |
| `volume_profile_matrix_v6` | 自適應成交量分佈矩陣 |
| `liq_sweep_dynamic_regime_v6` | 動態體制流動性掃蕩 |
| `LiquidityTransferEngine_v6` | 機構流動性抓取與 DOL |

## Deep Reinforcement Learning（深度強化學習，1） — NEW v26.0526

| 策略 | 說明 |
|------|------|
| `TnSovereignNeuraRLV6` | Dueling DQN + Prioritized Experience Replay + 雙網路架構 |

## Matrix & Machine Learning（矩陣與機器學習，10）

| 策略 | 說明 |
|------|------|
| `matrix_knn_ml_v6` | 矩陣 KNN 鄰近演算法 |
| `knn_matrix_ml_v6` | KNN 矩陣 ML（替代實作） |
| `ml_matrix_ensemble_v6` | ML 矩陣集成系統 |
| `monte_carlo_risk_matrix_v6` | 蒙地卡羅風險模擬矩陣 |
| `matrix_ols_stat_arb_v6` | 矩陣 OLS 統計套利 |
| `causal_matrix_weights_v6` | 因果權重演算矩陣 |
| `causal_backtracking_v6` | 因果回溯策略 |
| `TnSovereignLorentzianV6` | Lorentzian 分類 + 多維特徵因果審計 |
| `TnSovereignEntropyCausalityV6` | Transfer Entropy 因果策略 |
| `TnSovereignTopologicalSutureV6` | 拓撲連接性策略 |

## Multi-Agent, Swarm & Macro（多智能體、蜂群與宏觀，11）

| 策略 | 說明 |
|------|------|
| `federated_consensus_sovereign_v6` | 聯邦共識主權投票 |
| `federated_swarm_voting_v6` | 聯邦蜂群投票 |
| `swarm_modular_executor_v6` | 蜂群模組化執行器 |
| `dynamic_sharpe_voting_v6` | 動態 Sharpe 投票 |
| `multi_agent_of_ensemble_v6` | 多代理人集成訂單流 |
| `momentum_swarm_sovereign_v6` | 多資產動能輪動 |
| `TnSovereignLiquidityMatrixV6` | 適應性宏觀錨定矩陣 |
| `TnSovereignSignalForgeV6` | ML 驅動多模型主權 |
| `TnSovereignSignalForgeV20` | 7 因子適應性集成 |
| `macro_modeling_sovereign_v6` | 宏觀環境狀態機 |
| `sentiment_macro_sovereign_v6` | 情緒宏觀主權策略 |

### Optimization & Portfolio（優化與組合，6）

| 策略 | 說明 |
|------|------|
| `yield_spread_sovereign_v6` | 美債收益率差監測 |
| `markowitz_portfolio_sovereign_v6` | Markowitz 最小變異組合 |
| `tn_max_sharpe_sovereign_v6` | 最大 Sharpe 比率優化 |
| `multi_asset_corr_hedging_v6` | 多資產相關性避險 |
| `multilateral_sovereign_corr_v6` | 多邊主權相關性 |
| `volatility_regime_sovereign_v6` | 波動率體制策略 |

## Core Library & Utility（核心庫與工具，5）

| 策略 | 說明 |
|------|------|
| `lib_sovereign_logic_v6` | 主權邏輯庫（過濾器 + 風險對位組件） |
| `template_v6` | 策略模板 |
| `TnSovereignAliceV6` | Alice 5 法台股策略 |
| `EMA_Bars_v6` | EMA + 時間出場策略 |
| `triple_confirmation_sovereign_v6` | 三重確認主權策略 |

## DCA & Webhook（DCA 網格與 Webhook 橋接，1）

| 策略 | 說明 |
|------|------|
| `TnSovereignDcaWebhookV6` | DCA 網格引擎 + BBW 波動率過濾 + JSON Webhook 輸出（獵取自 ggamer5555） |

---

*註：所有策略具備完整因果說明文件（.md），一對一對應每個 .pine 檔案。*