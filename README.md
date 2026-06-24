# TeleNexus Sovereign Trading Systems (v6)

> **"Trading is not a game of chance, but a disciplined audit of causal reality."**

[![Pine Script v6](https://img.shields.io/badge/Script-Pine_v6.0-2962FF.svg)](https://www.tradingview.com/pine-script-docs/en/v6/Introduction.html)
[![Sovereign Governance](https://img.shields.io/badge/Governance-TeleNexus_Sovereign-green.svg)](https://github.com/raybird/telenexus)
[![Dashboard](https://img.shields.io/badge/Live-Sovereign_Dashboard-blue.svg)](https://raybird.github.io/pine-trading-strategies/)

## Live Disclosure
本專案進度與策略矩陣即時同步至：
**[TeleNexus Sovereign Dashboard](https://raybird.github.io/pine-trading-strategies/)**

---

## Spirit of TeleNexus

本儲存庫是 **TeleNexus Studio** 的實體化量化資產庫。拒絕傳統黑盒開發，主張**主權交易 (Sovereign Trading)**：每一行代碼都是對市場因果結構的深度審計。

1. **Causal Sovereignty** — 策略內建因果審計狀態表，決策基於邏輯必然，非機率疊加。
2. **Physical Alignment** — 版號（vYY.MMDD.HHMM）與 Git 提交精準鎖定 CST (UTC+8)。
3. **Deterministic Evolution** — 透過自動化獵頭排程自主維護，每日自演化。

---

## Technical Pillars

- **Pine Script v6**：全量實裝 UDT、Matrix、Collections。
- **MIAP Protocol**：整合 TeleNexus 記憶系統，跨會話情境感知。
- **Multi-Agent Consensus**：聯邦共識 + 蜂群投票，多維過濾降低單點失效風險。

---

## Repository Map

- **[`/strategies`](./strategies/README.md)** — 163 個已實體化主權策略，分 14 大類（v26.0625.0630 更新）
- **[`/lib`](./strategies/lib_sovereign_logic_v6.pine)** — 核心邏輯庫（主權過濾與風險對位組件）
- **[`/docs`](./docs/)** — 視覺化儀表板

---

## 策略全分類一覽

| 分類 | 數量 | 說明 |
|------|------|------|
| **Sovereign Core** | 12 | 基礎主權框架與多時框日內系統 |
| **Trend & Momentum** | 15 | 趨勢追蹤、動量振盪、均線系統、WaveTrend v4 |
| **Mean Reversion & Oscillator** | 17 | 均值回歸、超買超賣反轉、Z-Score 波動率反轉、PDH/PDL 反轉、IB 均值回歸 |
| **Volatility & Breakout** | 21 | 波動率突破、壓縮釋放、通道策略、多時段 ORB、體制自適應、NQ NY OPR 突破 |
| **Market Structure & Price Action** | 32 | SMC/ICT、波段結構、FVG/IFVG、訂單塊、CISD 結構破壞、反轉品質分級、價值區拒絕、Melgo 六態分類、PO3 三相位引擎、IB+VWAP 匯流、黃金 IB 突破拉回 |
| **Volume & Order Flow** | 12 | 足跡圖、失衡偵測、流動性獵取、機率評分流動性磁鐵 |
| **Deep Reinforcement Learning** | 1 | Dueling DQN + NeuraLib 強化學習 |
| **Matrix & Machine Learning** | 10 | KNN、OLS、因果權重、蒙地卡羅 |
| **Multi-Agent, Swarm & Macro** | 12 | 聯邦共識、蜂群、宏觀建模、組合優化、成對相關性發散 |
| **Optimization & Portfolio** | 7 | 組合優化、風險管理、相關性對沖 |
| **DCA & Webhook** | 1 | DCA 網格引擎 + BBW 波動率過濾 + JSON Webhook 橋接 |
| **PropFirm / Challenge** | 1 | PropFirm 挑戰賽超防禦策略（三層風控 + SMC 結構） |
| **Signal Quality & Fakeout Prevention** | 2 | 信號品質與防假突破過濾 |
| **Core Library & Utility** | 5 | 主權邏輯庫與策略模板、工具 |
| **Total** | **163** | 主權策略矩陣（v26.0625.0630 更新） |


> **最新加入（v26.0625.0630）**: 獵頭審計 #104 — GitHub 60+ 儲存庫全數檢索（跨 2 頁搜尋結果 + `"strategy(" v6` 補集查詢 + PineGen-AI 14 倉二次驗證）。新檢索 repos: jayadevrana/pinescript-custom-confluence-futures-strategy-v6 為 NSE 印度市場合流策略（Supertrend + EMA + MACD + RSI + RS + ADX + HA + OI），基礎邏輯無移植價值；sametbarbaros-dev/PineScript-Architect 為 React/TypeScript AI Studio 工具非策略實體；其餘所有 repos 均已在過去審計中覆蓋無全新 strategy() 實體；TradingView 社群 Cloudflare 持續阻擋無法存取；維持 163 策略物理對位；Dashboard 同步更新
>
> **最新加入（v26.0624.1830）**: 獵頭審計 #103 — GitHub 60+ 儲存庫全數檢索（跨 4 頁搜尋結果 + 多組查詞交叉驗證）。新檢索 repos: codenamedevan/pinescriptv6 為 Pine Script v6 文件知識庫非策略實體；Zkalish/pinescriptv6 同為 LLM 文件庫無獨立策略；odilsonriquelme/pinescript-v6 為 PDF 文件無實體；Alephxxii/Pinescript-v6 含 ICT Scalp indicator() 非 strategy() 實體；blablablasealsaresoft/US30 為 Python 為主的 ORB 專案無 Pine Script strategy() 實體；damianpitt/capital41-indicators、mazetezr/tradingview-indicator、hungpixi/pinescript-ict 等均為 indicators 集合無獨立策略；TradingView 社群 Cloudflare 持續阻擋無法存取；維持 163 策略物理對位；Dashboard 同步更新
>
> **最新加入（v26.0623.1830）**: 獵頭審計 #101 — GitHub 55+ 儲存庫全數檢索（新檢索 repos: VolodymyrFilias/feels-indicators 為 FEELS 指標集合（Air Pocket Profile / Confluence Pivot Zones / Support-Resistance Zones），均為 indicator() 非 strategy() 實體無移植價值；alexhowa53/pinescript-v6-toolkit 404 倉庫已下架；chris-c-thomas/chrd-tradingview-pine-scripts 為技術指標集合無獨立策略實體）；TradingView 社群 Cloudflare 阻擋無法存取；維持 163 策略物理對位；Dashboard 同步更新
>
> **最新加入（v26.0623.0630）**: 獵頭審計 — GitHub 55+ 儲存庫 + TradingView 社群全數檢索（新檢索 repos: randomwalkhan/Short-Term-Reversal-Strategy 為 Python 量化研究非 Pine Script 實體；EvertonTomalok/splinter 為多智能體編碼框架非策略實體；DexWilder/algo-lab 為 Pine→Python 轉換工程無原始 .pine 檔案；alvin-forex/trade-strategy-analyzer、adamopenbook/strategy-dashboard、rexlau-prog/zynerise-btc-bot 均為 HTML 儀表板非策略實體）；TradingView 社群無全新 v6 strategy 實體；維持 163 策略物理對位；Dashboard 同步更新
>
> **最新加入（v26.0622.1830）**: 獵頭審計 — GitHub 55+ 儲存庫全數檢索（新檢索 repos: FRX132/Trading_View_Indicator 為 OOTM Session Sweeps & Breakouts 策略已有 TnSovereignSessionQuantV6/TnSovereignOrbMultiSessionV6 覆蓋；Capitalpro123/StrategyA_Engulfing 為基礎吞噬 K 線策略已有 TnSovereignReversalEngineV6 覆蓋；Capitalpro123/StrategyA_Marketstructure 與 StrategyA_ichimoku 均已有對應 SMC/Ichimoku 策略覆蓋；piazzolimichele1/Pinescript-V6 含 6 款基礎策略（Ichimoku/Engulfing/Range Breakout）均無移植價值；hamedator/advanced-pinescript-strategy-v6 為 demo 版無完整邏輯；JackSmack1971/traderjack-pinescript-v6-sripts 為 indicators 集合無獨立策略；mrdungx2603/Tradingview-Pine-Scripts 為初始模板倉無實際 .pine 策略）；維持 163 策略物理對位；Dashboard 同步更新
>
> **最新加入（v26.0622.0630）**: 獵頭審計 — GitHub 55+ 儲存庫全數檢索（新檢索 repos: jcornierfra/TradingView_Strategy_JCO_OPR_Breakout NQ NY Session OPR 突破策略，移植為 `TnSovereignNqOprBreakoutV6`；yaniv1157/breakout-confluence-scanner 為 7 策略匯流掃描指標非策略實體；PineGen-AI/ml-inspired-adaptive-momentum-strategy 與 volatility-squeeze-expansion-strategy 為基礎實作已有對應策略覆蓋；SimoneGitter/AdvancedMA-Toolkit 為 MA 工具庫無獨立策略）；維持 163 策略物理對位；Dashboard 同步更新
>
> **最新加入（v26.0620.1830）**: 獵頭審計 — GitHub 55 儲存庫全數檢索（含新檢索 repos: FaustoS88/Pydantic-AI-Pinescript-Expert RAG agent 非策略實體、Aksee123/nq1_Scalping_Strategy 自訂 VP scalping 已有 TnSovereignVolumeProfileScalpV6 覆蓋、rajitha-yasas/Pine-Script-v6-Trading-Strategy 基礎多指標已有對應策略）、TradingView 社群無法存取；維持 162 策略物理對位；Dashboard 同步更新
>
> **最新加入（v26.0619.1830）**: 獵頭審計 — GitHub 55 儲存庫全數檢索（含 Prat617/strategic 7 款 NQ/ES/GC Elite 策略系統），新增 5 款主權化策略：`TnSovereignZScoreReversionV6`（Z-Score 波動率反轉）、`TnSovereignIBVWAPConfluenceV6`（IB+VWAP 品質評分匯流）、`TnSovereignPDHPDLFadeV6`（前日高/低均值回歸）、`TnSovereignGoldIBRetracementV6`（黃金 IB 突破拉回）、`TnSovereignIBMeanReversionV6`（IB 日型分類均值回歸）；162 策略物理對位；Dashboard 同步更新
>
> **最新加入（v26.0619.0630）**: `tn_ifvg_cisd_double_confirm_v6` — TeleNexus 主權 IFVG+CISD 雙重確認入場策略（Inverse Fair Value Gap 翻轉偵測 + Change in State of Delivery 結構破壞追蹤 + 流動性掃蕩過濾 + EMA 趨勢濾網 + ATR 風控），移植自 aleks-drozy/fyp-trading-strategy (Maynooth University FYP 2026)
>
> **最新加入（v26.0618.1830）**: `TnSovereignPowerOfThreeV6` — TeleNexus 主權 PO3 三相位引擎（Accumulation→Manipulation→Distribution 完整狀態機 + 歷史頻率統計），移植自 FEELS Power of Three v1.5
>
> **最新加入（v26.0618.1830）**: `TnSovereignLiquidityMagnetV6` — TeleNexus 主權流動性磁鐵機率引擎（四維評分 + Pool 排名 + 磁鐵拉力 + 可視化池區），移植自 FEELS Liquidity Magnet v1.6.4
>
> **最新加入（v26.0612.1830）**: `tn_opening_range_magnet_v6` — TeleNexus 主權開盤區間磁鐵策略（OR High/Low 磁鐵效應 + 價格漂移回測入場 + NR7/缺口/趨勢過濾 + ATR 風控 + 每日虧損限制），移植自 biagDev/nq-magnet-framework (NQ Magnet Framework v2/v3)
>
> **最新加入（v26.0609.1830）**: 獵頭審計 — GitHub 55 儲存庫全數檢索（含 ggamer5555/Pinescript-v6-strategy-with-Json-Webhook-output-example DCA+BBW+Webhook 策略已有 `TnSovereignDcaWebhookV6` 覆蓋；reggytrades/pine-script-workspace 為 v5/v6 混合 snippets 無獨立策略；PineGen-AI 14 倉全數檢視 modular-trend-pullback 與 pivot-based-dynamic-trend 均為基礎 EMA+ATR 已有對應策略覆蓋）+ TradingView 社群無法存取（Cloudflare 阻擋）；Dashboard 同步更新
>
> **最新加入（v26.0607.1830）**: 獵頭審計 — GitHub 55 儲存庫全數檢索（含 PineGen-AI 系列 14 倉僅 README 無 .pine 實作、Viprasol-Tech/pine-script-strategy 為 EMA 交叉基礎策略無移植價值）+ TradingView 社群無全新 v6 策略；維持 153 策略物理對位；Dashboard 同步更新
>
> **最新加入（v26.0607.0630）**: 獵頭審計 — GitHub 55 儲存庫全數檢索（含新增 Viprasol-Tech/pine-script-strategy、NizamAhmad233/pine-script-ai-generator、s7cret/openpine-trading，均無全新可移植策略）+ TradingView 社群無全新 v6 策略；維持 153 策略物理對位；Dashboard 同步更新
>
> **最新加入（v26.0606.1830）**: 獵頭審計 — GitHub 53 儲存庫 + TradingView 社群全數檢索，無全新可移植策略；維持 153 策略物理對位；Dashboard 同步更新
>
> **最新加入（v26.0606.0630）**: `TnSovereignViopSessionV6` — TeleNexus 主權 VIOP 時段策略（EMA 9/21 交叉 + 09:30–18:15 時段規訓 + ATR SL/TP + 收盤強制平倉），移植自 trugurpala/pinescriptv6 (VIOP Session Strategy)
>
> **最新加入（v26.0606.0630）**: `TnSovereignStochDivergenceV6` — TeleNexus 主權 Stochastic 背離策略（5-bar pivot 多空背離偵測 + %D 背離線 + 破裂移除），移植自 JoelPasapera/Strategies-in-Pine-Script-v6 (Stochastic Divergence Strategy)
>
> **最新加入（v26.0606.0630）**: `TnSovereignDonchianBreakoutV6` — TeleNexus 主權 Donchian 突破策略（時間觸發 Buy Stop + 25-bar Donchian 通道 + 通道下緣動態停損），移植自 JoelPasapera/Strategies-in-Pine-Script-v6 (Donchian Breakout Strategy)
>
> **最新加入（v26.0605.0630）**: `tn_pair_corr_divergence_v6` — TeleNexus 成對相關性 Z-Score 發散策略（雙資產回報擴散的 Z-Score 均值回歸 + EMA 趨勢濾網 + RSI/MACD 動量確認 + 相關性門檻 + ATR 風控），移植自 PineGen-AI/pair-correlation-divergence-strategy

> **最新加入（v26.0531.1830）**: `TnSovereignScalpingProV6` — TeleNexus Sovereign Scalping Pro V6（4 模式風險縮放 + 11 項因果優化模組 + 市場結構引擎 CHoCH/BOS/IDM + Kelly 倉位 + 動態 R:R + 波動體制自適應），移植自 KEBOSLABS/scalping-pro-strategy (Scalping Pro v3)
> 
> **最新加入（v26.0531.0630）**: `tn_melgo_sequence_v6` — 六態價格結構分類策略（HL2/HLC3/OHLC4 排序狀態機 + MTF 共識投票 + Spread 信心閾值），移植自 jeffreymelgo/melgo-sequence (SSRN 6658238)
> 
> **最新加入（v26.0531.0630）**: `tn_wavetrend_v4_v6` — WaveTrend v4 動量反轉策略（多時框 OS/OB + Gate A/C/G 品質過濾 + ATR 風控），移植自 casoon/pine-scripts (WavesUnchained)
> 
> **上版（v26.0529.1830）**: `v6_stochastic_divergence` — Stochastic 背離偵測策略（5-bar pivot + %D 多空背離 + SL/TP 風控），移植自 JoelPasapera/Strategies-in-Pine-Script-v6
> 
> **上版（v26.0528.1830）**: `TnSovereignPropFirmUltraV6` — TeleNexus PropFirm 主權超防禦策略（三層風控 + SMC 結構引擎 + 動態風險係數），移植自 thesenegalesehitch/Pine-Script (QuantAlgo propfirm-ultra-strategy)
>
> **上版（v26.0528.0630）**: `tn_fakeout_signal_quality_v6` — 4 層信號品質過濾（成交量 + HTF 趨勢 + ATR 波動帶 + 條形結構），移植自 trugurpala/pinescriptv6
>
> **上版（v26.0527.1830）**: `swarm_modular_executor_v6` — TeleNexus 蜂群聯邦共識引擎（4 元蜂群 + 民主投票 + 三級規訓）
>
> 各策略詳細說明請見 [`/strategies/README.md`](./strategies/README.md)

---

## 免責聲明

本專案內容僅供學術研究與技術開發參考，不構成任何形式的投資建議。

---

*Created and evolved by Raybird via TeleNexus Studio.*