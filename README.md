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

- **[`/strategies`](./strategies/README.md)** — 135 個已實體化主權策略，分 10 大類
- **[`/lib`](./strategies/lib_sovereign_logic_v6.pine)** — 核心邏輯庫（主權過濾與風險對位組件）
- **[`/docs`](./docs/)** — 視覺化儀表板

---

## 策略全分類一覽

| 分類 | 數量 | 說明 |
|------|------|------|
| **Sovereign Core** | 12 | 基礎主權框架與多時框日內系統 |
| **Trend & Momentum** | 15 | 趨勢追蹤、動量振盪、均線系統、WaveTrend v4 |
| **Mean Reversion & Oscillator** | 14 | 均值回歸、超買超賣反轉 |
| **Volatility & Breakout** | 19 | 波動率突破、壓縮釋放、通道策略、多時段 ORB、體制自適應 |
| **Market Structure & Price Action** | 21 | SMC/ICT、波段結構、FVG、訂單塊、反轉品質分級、價值區拒絕、Melgo 六態分類 |
| **Volume & Order Flow** | 11 | 足跡圖、失衡偵測、流動性獵取 |
| **Deep Reinforcement Learning** | 1 | Dueling DQN + NeuraLib 強化學習 |
| **Matrix & Machine Learning** | 10 | KNN、OLS、因果權重、蒙地卡羅 |
| **Multi-Agent, Swarm & Macro** | 11 | 聯邦共識、蜂群、宏觀建模、組合優化 |
| **Optimization & Portfolio** | 7 | 組合優化、風險管理、相關性對沖 |
| **DCA & Webhook** | 1 | DCA 網格引擎 + BBW 波動率過濾 + JSON Webhook 橋接 |
| **PropFirm / Challenge** | 1 | PropFirm 挑戰賽超防禦策略（三層風控 + SMC 結構） |
| **Signal Quality & Fakeout Prevention** | 2 | 信號品質與防假突破過濾 |
| **Core Library & Utility** | 5 | 主權邏輯庫與策略模板、工具 |
| **Total** | **144** | 主權策略矩陣 |


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