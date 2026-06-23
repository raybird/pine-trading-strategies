# Strategies Catalog

TeleNexus 旗下所有已實體化的 Pine Script v6 策略，按技術邏輯分類。

---

## Sovereign Core（主權核心，13）

| 策略 | 說明 |
|------|------|
| `tn_multi_audit_sovereign_v6` | 多維因果審計主權系統 |
| `tn_multi_factor_sovereign_v6` | 多因子主權策略 |
| `tn_session_sovereign_v6` | 時段規訓主權策略 |
| `tn_sovereign_audit_v6` | 因果審計主權系統 |
| `tn_sovereign_mtf_dual_layer_v6` | 雙層 MTF 主權策略 |
| `tn_sovereign_mtf_trend_v6` | MTF 趨勢主權策略 |
| `tn_sovereign_v6` | 基礎主權交易框架 |
| `tn_universal_sovereign_v6` | 通用型主權規訓策略 |
| `TnSovereignMtfIntradayV6` | 多時框因果對位日內策略 |
| `TnSovereignMtfViopV6` | MTF VIOP，時序審計特徵 |
| `TnSovereignMultiCausalityV6` | 三層因果共振趨勢追蹤 |
| `TnSovereignSessionQuantV6` | 時空對位開盤區間突破策略 |
| `TnSovereignHFTEngineV6` | 機構級 HFT 機率評分引擎 |

## Trend & Momentum（趨勢與動量，16）

| 策略 | 說明 |
|------|------|
| `MtfTrendSovereignV6` | 多時框趨勢主權 |
| `tn_sovereign_katana_flow_v6` | 雙平滑範圍濾波器 (Twin Range Filter) 趨勢策略 |
| `tn_sovereign_vamo_v6` | VAMO 波動調整動量振盪器 |
| `tn_triple_momentum_sovereign_v6` | 三重動量主權策略 |
| `TnSovereignAdxTrendV6` | ADX 趨勢強度審計 + ATR 風險對位 |
| `TnSovereignHMAV6` | 雙重 HMA 對位 + 成交量能量審計 |
| `TnSovereignMacdV6` | MACD + 動能斜率審計 + 200 EMA 過濾 |
| `TnSovereignOptimizedTrendV6` | 多尺度 EMA 交叉 + 成交量因果過濾 |
| `TnSovereignScalpingProV6` | 4 模式風險縮放 Scalping 策略 |
| `TnSovereignSupertrendV6` | 多維趨勢地板 (200/50 EMA) 超級趨勢 |
| `TnSovereignSupertrendVolV6` | Supertrend ATR + 成交量放大確認 |
| `TnSovereignTripleEmaV6` | 5/13/34 EMA 對位 + 200 EMA 全球地板 |
| `TnSovereignVAMOStrategyV6` | VAMO 波動調整動量策略（完整版） |
| `TnSovereignVortexV6` | 渦流極性審計 + 200 EMA 過濾 |
| `tn_wavetrend_v4_v6` | WaveTrend v4 波動交易策略 |
| `tn_smooth_trend_radar_v6` | 雙平滑超級趨勢 + 樞軸拒絕雷達 |

## Mean Reversion & Oscillator（均值回歸與振盪指標，18）

| 策略 | 說明 |
|------|------|
| `RsiMeanReversionSovereignV6` | Bollinger + RSI 均值回歸 |
| `tn_stoch_causal_divergence_v6` | Stochastic 因果背離與結構審計 |
| `TnSovereignCCIV6` | 雙重 CCI 對位 + 200 EMA 趨勢地板 |
| `TnSovereignCMOV6` | CMO 動能背離 + 極端區域審計 |
| `TnSovereignFisherV6` | 費雪轉換極性審計 + 200 EMA 過濾 |
| `TnSovereignReversalEngineV6` | 流動性掃蕩與分形熵值反轉引擎 |
| `TnSovereignRsiAtrV6` | RSI 動能門檻 + ATR 動態風險管理 |
| `TnSovereignSTCV6` | 謝夫趨勢週期 + 200 EMA 過濾 |
| `TnSovereignStochCausalDivV6` | 隨機指標因果背離 + 熱力學相位規訓 |
| `TnSovereignStochV6` | 隨機指標區域審計 + 200 EMA 過濾 |
| `TnSovereignVwapRegimeV6` | VWAP Regime 偏差策略 |
| `TnSovereignVWAPV6` | 動態錨定 VWAP + 標準差通道均值回歸 |
| `TnSovereignWaveTrendV20` | WaveTrend 熱力學反轉 |
| `v6_stochastic_divergence` | 隨機指標背離 (v6 移植) |
| `TnSovereignStochDivergenceV6` | Stoch + MACD 雙重背離偵測 |
| `TnSovereignZScoreReversionV6` | Z-Score 波動率反轉（Session VWAP + 耗竭 K 線 + ATR 百分位體制），移植自 Prat617/strategic |
| `TnSovereignPDHPDLFadeV6` | 前日高/低均值回歸反轉（PDH/PDL + VWAP 偏見 + Swing Stop），移植自 Prat617/strategic |
| `TnSovereignIBMeanReversionV6` | IB 均值回歸反轉（日型分類 + 延伸區 Fade + MA 濾網），移植自 Prat617/strategic |

## Volatility & Breakout（波動率與突破，25）

| 策略 | 說明 |
|------|------|
| `adaptive_vol_regime_sovereign_v6` | 百分 rank 自適應波動率切換系統 |
| `tn_asymmetric_swing_v6` | 不對稱波段策略 |
| `tn_compression_expansion_v6` | ATR 壓縮 → 膨脹突破 |
| `tn_sovereign_donchian_v6` | 成交量驗證 Donchian 突破 |
| `TnSovereignAdaptiveRegimeV6` | ATR 波動率狀態切換 + 壓縮擴張 + 假突破過濾（PineGen-AI 融合） |
| `TnSovereignAdaptiveRiskRegimeV6` | ATR 波動體制與動態 SL/TP 調整 |
| `TnSovereignBbBreakoutV6` | Bollinger 突破 + Keltner 擠壓 + 成交量審計 |
| `TnSovereignBreakoutConfluenceV6` | 突破共鳴策略 |
| `TnSovereignChandelierV6` | Chandelier 止損 + 200 EMA 趨勢 |
| `TnSovereignDonchianV6` | 唐奇安通道突破 + 時序執行規訓 |
| `TnSovereignGapFillOpeningRangeV6` | 跳空填補與開盤區間突破 |
| `TnSovereignKeltnerV6` | Keltner 通道突破 + ADX 動能過濾 |
| `TnSovereignOrbMultiV6` | 多模型 ORB 開盤區間突破 |
| `TnSovereignThermodynamicBreakoutV20` | 熱力學膨脹突破策略 |
| `TnSovereignThermodynamicSqueezeV20` | 熱力學擠壓膨脹策略 |
| `TnSovereignVolumeProfileScalpV6` | Volume Profile 精準 scalp |
| `tokyo_breakout_v6_refined` | 東京時段突破策略 |
| `TnSovereignOrbMultiSessionV6` | 多時段開盤區間突破 |
| `TnSovereignDonchianBreakoutV6` | 唐奇安通道突破 |
| `tn_adaptive_risk_regime_v6` | 自適應風險體制突破 |
| `tn_chandelier_flip_radar_v6` | 5 級趨勢 + ATR 追蹤反轉雷達 |
| `tn_pinegen_vol_exp_fake_break_v6` | 波動擴張 + 假突破過濾 (PineGen 移植) |
| `tn_pinegen_vol_switch_regime_v6` | 波動體制切換 (PineGen 移植) |
| `tn_opening_range_magnet_v6` | 開盤區間磁鐵效應策略（OR High/Low 磁鐵 + 價格漂移回測 + NR7/缺口過濾），移植自 biagDev/nq-magnet-framework |
| `TnSovereignNqOprBreakoutV6` | NQ NY 時段 OPR 突破策略（可配置區間 + RSI/EMA 選擇性過濾 + 擺動止損 + 每日一單止損紀律），移植自 jcornierfra/TradingView_Strategy_JCO_OPR_Breakout |

## Market Structure & Price Action（市場結構與價格行為，32）

| 策略 | 說明 |
|------|------|
| `AdvancedSwingStrategyV6` | 進階波段策略（精簡版） |
| `fvg_orderblock_sovereign_v6` | FVG + 訂單塊對位 |
| `smc_matrix_sovereign_v6` | SMC 矩陣主權策略 |
| `smc_sovereign_v6` | 聰明錢概念 (SMC) 主權化 |
| `tn_sovereign_adv_swing_v6` | 主權進階波段 |
| `tn_sovereign_darvas_v6` | 自動化 Darvas 箱體規訓 |
| `tn_sovereign_fibonacci_v6` | 結構性 Fibonacci 回撤系統 |
| `tn_sovereign_ichimoku_v6` | Ichimoku 主權策略 |
| `tn_sovereign_ict_smc_v6` | ICT/SMC 融合主權策略 |
| `tn_sovereign_market_structure_v6` | 市場結構主權策略 |
| `tn_sovereign_mtf_swing_v6` | 多時框擺動高低點與 CHoCH 偵測指標 |
| `TnSovereignAdvancedSwingV6` | 多維時序對位進階波段 |
| `TnSovereignFlowZoneV6` | 波動率突破與多層流動性匯流區 |
| `TnSovereignImbalanceConfluenceV6` | FVG + 訂單失衡多維匯流 |
| `TnSovereignMarketStructureV20` | 市場結構 + 熱力學策略 |
| `XauusdIntradayTrendPullbackV6` | 黃金日內趨勢拉回 |
| `ZzcCorridorSovereignV6` | 擠壓偵測 + Wyckoff 審計波段走廊 |
| `ZzcMarketStructureSovereignV6` | ZZC 波段結構主權策略 |
| `TnSovereignVeinReversalV6` | 靜脈反轉 + 流動性掃蕩 |
| `tn_melgo_sequence_v6` | Melgo 序列結構策略 |
| `tn_value_area_rejection_v6` | 價值區拒絕策略 |
| `TnSovereignIctComboV6` | ICT 組合策略 |
| `TnSovereignIctSmcComboV6` | ICT/SMC 融合組合策略 |
| `TnSovereignIctSurgicalV20` | ICT 外科手術式 V20 策略 |
| `TnSovereignIctV6` | ICT 核心策略 |
| `TnSovereignMultiConfluenceV6` | ICT 多重匯聚主權框架 |
| `TnSovereignSMCV6` | SMC 主權策略 |
| `tn_pinegen_lvn_reject_accept_v6` | LVN 拒絕/接受 (PineGen 移植) |
| `TnSovereignPowerOfThreeV6` | PO3 三相位引擎（Accumulation→Manipulation→Distribution），移植自 FEELS Power of Three v1.5 |
| `tn_ifvg_cisd_double_confirm_v6` | IFVG（反轉 FVG）+ CISD（結構破壞）雙重確認入場，移植自 aleks-drozy/fyp-trading-strategy |
| `TnSovereignIBVWAPConfluenceV6` | IB+VWAP 品質評分匯流（10 分制 IB 寬度 + 延伸 + 拒絕 K 線 + VWAP 接近度 + 動態口數），移植自 Prat617/strategic |
| `TnSovereignGoldIBRetracementV6` | 黃金 IB 突破拉回（IB 範圍 % 過濾 + 突破偵測 + 回撤入場 + 成交量確認），移植自 Prat617/strategic |

## Volume & Order Flow（成交量與訂單流，15）

| 策略 | 說明 |
|------|------|
| `footprint_entropy_sovereign_v6` | 訂單流熵值分析 |
| `footprint_explorer_v6` | 實體買賣壓力感知 |
| `footprint_liquidity_sweep_v6` | 足跡圖流動性獵取 |
| `liq_sweep_dynamic_regime_v6` | 動態體制流動性掃蕩 |
| `LiquidityTransferEngine_v6` | 機構流動性抓取與 DOL |
| `of_imbalance_matrix_map_v6` | 訂單流失衡矩陣地圖 |
| `stacked_imbalance_sovereign_v6` | 堆疊失衡主權策略 |
| `tn_footprint_imbalance_v6` | 足跡圖失衡偵測 |
| `TnSovereignFootprintPOCV6` | 足跡圖 POC 突破 + 機構意圖審計 |
| `TnSovereignVolumeDeltaV6` | 累積 Delta 背離偵測 + 200 EMA 過濾 |
| `volume_profile_matrix_v6` | 自適應成交量分佈矩陣 |
| `TnSovereignLiquidityHuntV6` | 流動性獵取 + 機構位移確認 |
| `TnSovereignViopSessionV6` | VIOP 時序審計時段策略 |
| `tn_liquidity_sovereign_v6` | 4 層因果對位流動性審計 |
| `TnSovereignLiquidityMagnetV6` | 機率評分流動性磁鐵引擎（四維權重 + Pool 排名），移植自 FEELS Liquidity Magnet v1.6.4 |

## Deep Reinforcement Learning（深度強化學習，1）

| 策略 | 說明 |
|------|------|
| `TnSovereignNeuraRLV6` | Dueling DQN + Prioritized Experience Replay + 雙網路架構 |

## Matrix & Machine Learning（矩陣與機器學習，10）

| 策略 | 說明 |
|------|------|
| `causal_backtracking_v6` | 因果回溯策略 |
| `causal_matrix_weights_v6` | 因果權重演算矩陣 |
| `knn_matrix_ml_v6` | KNN 矩陣 ML（替代實作） |
| `matrix_knn_ml_v6` | 矩陣 KNN 鄰近演算法 |
| `matrix_ols_stat_arb_v6` | 矩陣 OLS 統計套利 |
| `ml_matrix_ensemble_v6` | ML 矩陣集成系統 |
| `monte_carlo_risk_matrix_v6` | 蒙地卡羅風險模擬矩陣 |
| `TnSovereignEntropyCausalityV6` | Transfer Entropy 因果策略 |
| `TnSovereignLorentzianV6` | Lorentzian 分類 + 多維特徵因果審計 |
| `TnSovereignTopologicalSutureV6` | 拓撲連接性策略 |

## Multi-Agent, Swarm & Macro（多智能體、蜂群與宏觀，12）

| 策略 | 說明 |
|------|------|
| `dynamic_sharpe_voting_v6` | 動態 Sharpe 投票 |
| `federated_consensus_sovereign_v6` | 聯邦共識主權投票 |
| `federated_swarm_voting_v6` | 聯邦蜂群投票 |
| `macro_modeling_sovereign_v6` | 宏觀環境狀態機 |
| `momentum_swarm_sovereign_v6` | 多資產動能輪動 |
| `multi_agent_of_ensemble_v6` | 多代理人集成訂單流 |
| `sentiment_macro_sovereign_v6` | 情緒宏觀主權策略 |
| `swarm_modular_executor_v6` | 蜂群模組化執行器 |
| `TnSovereignLiquidityMatrixV6` | 適應性宏觀錨定矩陣 |
| `TnSovereignSignalForgeV20` | 7 因子適應性集成 |
| `TnSovereignSignalForgeV6` | ML 驅動多模型主權 |
| `tn_pair_corr_divergence_v6` | 配對相關性背離偵測 |

## Optimization & Portfolio（優化與組合，7）

| 策略 | 說明 |
|------|------|
| `adaptive_risk_matrix_v6` | 2D 矩陣環境感知風險自適應調節 |
| `markowitz_portfolio_sovereign_v6` | Markowitz 最小變異組合 |
| `multi_asset_corr_hedging_v6` | 多資產相關性避險 |
| `multilateral_sovereign_corr_v6` | 多邊主權相關性 |
| `tn_max_sharpe_sovereign_v6` | 最大 Sharpe 比率優化 |
| `volatility_regime_sovereign_v6` | 波動率體制策略 |
| `yield_spread_sovereign_v6` | 美債收益率差監測 |

## DCA & Webhook（DCA 網格與 Webhook 橋接，1）

| 策略 | 說明 |
|------|------|
| `TnSovereignDcaWebhookV6` | DCA 網格引擎 + BBW 波動率過濾 + JSON Webhook 輸出（獵取自 ggamer5555） |

## PropFirm / Challenge（自營與挑戰賽，1）

| 策略 | 說明 |
|------|------|
| `TnSovereignPropFirmUltraV6` | 三層風控自營防禦與完整 SMC 引擎 |

## Signal Quality & Fakeout Prevention（信號品質與假突破預防，7）

| 策略 | 說明 |
|------|------|
| `tn_fakeout_signal_quality_v6` | 4 層信號品質過濾器（成交量 + HTF 趨勢 + ATR 波動帶 + 條形結構），移植自 trugurpala/pinescriptv6 |
| `tn_sovereign_fakeout_v6` | 4 層因果審計與假突破過濾 |
| `TnSovereignFakeoutConfirmedV6` | 假突破確認策略 |
| `TnSovereignFakeoutFilterV6` | 假突破過濾策略 |
| `TnSovereignFakeoutV6` | 主權假突破偵測 |
| `tn_fakeout_filter_v6` | 4 層信號品質評分過濾 |
| `tn_fakeout_sovereign_v6` | Enum 狀態機因果假突破審計 |

## Core Library & Utility（核心庫與工具，5）

| 策略 | 說明 |
|------|------|
| `EMA_Bars_v6` | EMA + 時間出場策略 |
| `lib_sovereign_logic_v6` | 主權邏輯庫（過濾器 + 風險對位組件） |
| `template_v6` | 策略模板 |
| `TnSovereignAliceV6` | Alice 5 法台股策略 |
| `triple_confirmation_sovereign_v6` | 三重確認主權策略 |

---

*策略總數：163（v26.0624.0630 更新）*
