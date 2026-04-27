# 🌌 TeleNexus Sovereign Trading Systems (v6)

> **"Trading is not a game of chance, but a disciplined audit of causal reality."**

[![Pine Script v6](https://img.shields.io/badge/Script-Pine_v6.0-2962FF.svg)](https://www.tradingview.com/pine-script-docs/en/v6/Introduction.html)
[![Sovereign Governance](https://img.shields.io/badge/Governance-TeleNexus_Sovereign-green.svg)](https://github.com/raybird/telenexus)
[![Dashboard](https://img.shields.io/badge/Live-Sovereign_Dashboard-blue.svg)](https://raybird.github.io/pine-trading-strategies/)

## 🔗 實時披露 (Live Disclosure)
本專案的規訓進度與策略矩陣已即時同步至：
**[TeleNexus Sovereign Dashboard](https://raybird.github.io/pine-trading-strategies/)**

---

## 📖 核心精神 (The Spirit of TeleNexus)

本儲存庫是 **TeleNexus Studio** 的實體化量化資產庫。我們拒絕傳統量化開發中的「黑盒黑箱」，主張**主權交易 (Sovereign Trading)** 的核心理念。在這裡，每一行代碼都是一次對市場因果結構的深度審計。

### 1. 因果主權 (Causal Sovereignty)
我們認為，真正的交易優勢源於對市場微觀結構（如訂單流、流動性陷阱）的因果理解。所有策略均內建「因果審計狀態表」，確保買賣決策不僅是機率的疊加，更是邏輯的必然。

### 2. 物理對位 (Physical Alignment)
系統嚴格執行物理時間對位規訓。所有版本號（vYY.MMDD.HHMM）與 Git 提交軌跡均精準鎖定 **CST (UTC+8)**，確保數位資產在跨時空維度下具備無可爭議的因果連續性。

### 3. 確定性演化 (Deterministic Evolution)
本儲存庫由 TeleNexus AI 代理人透過「自動化獵頭排程」自主維護。從全球開源生態中擷取高信號邏輯，並依據 Pine Script v6 標準進行「主權化重寫」，實現資產庫的每日自演化。

---

## 🛠️ 技術支柱 (Technical Pillars)

- **Pine Script v6 標準**：全量實裝 UDT (User Defined Types)、Matrix (矩陣運算)、Collections (集合) 等高階語法，實現工業級的代碼封裝。
- **MIAP (記憶意圖宣告協定)**：整合 TeleNexus 的記憶系統，讓策略執行具備「跨會話」的情境感知能力。
- **多代理共識 (Multi-Agent Consensus)**：導入聯邦共識與蜂群投票邏輯，利用多維度過濾矩陣降低單點邏輯失效風險。

---

## 📂 儲存庫結構 (Repository Map)

- **[`/strategies`](./strategies/README.md)**：策略實體目錄。包含各類已實體化的主權交易系統清單。
    - **核心主權**：[`TnSovereignMtfViopV6.md`](./strategies/TnSovereignMtfViopV6.md)
    - **市場結構**：[`ZzcCorridorSovereignV6.md`](./strategies/ZzcCorridorSovereignV6.md)
    - **訂單流感知**：[`tn_footprint_imbalance_v6.md`](./strategies/tn_footprint_imbalance_v6.md)
    - **機器學習**：[`matrix_knn_ml_v6.md`](./strategies/matrix_knn_ml_v6.md)
- **[`/lib`](./strategies/lib_sovereign_logic_v6.pine)**：核心邏輯庫。定義了 TeleNexus 的主權過濾與風險對位標準組件。
- **[`/docs`](./strategies/README.md)**：策略的「因果說明書」索引。

---

## ⚖️ 免責聲明 (Disclaimer)

本專案內容僅供學術研究與技術開發參考，不構成任何形式的投資建議。市場交易存在極高風險，所有執行應由使用者在充分理解「主權風險管理協定」的前提下自主負責。

---
*Created and evolved by Raybird via TeleNexus Studio.*

### [v26.0420.0603] Zzc Corridor Sovereign v6
- **核心**: 整合擠壓偵測與 Wyckoff 審計的波段走廊主權策略。
- **技術**: Pine Script v6.0, 擠壓釋放邏輯, 實時審計 HUD。
- **狀態**: 已實體化至 `strategies/`。

### [v26.0420.0002] Tn Sovereign MTF VIOP v6
- **核心**: 雙層時序對位（1M/5M）與物理能量過濾規訓。
- **技術**: Pine Script v6.0, 非重繪 MTF, 實時審計 HUD。
- **狀態**: 已實體化至 `strategies/`。

### [v26.0419.1801] Tn Sovereign Advanced Swing v6
- **核心**: 多維時序對位（W/D/4H）與機構級因果過濾引擎。
- **技術**: Pine Script v6.0, 動態風險對位, 實時審計 HUD。
- **狀態**: 已實體化至 `strategies/`。
## v26.0427.0630 Updates
- Added `tn_sovereign_donchian_v6`: Volume-backed breakout strategy.
- Added `tn_sovereign_fibonacci_v6`: Time-anchored trend pullback strategy.

### [v26.0427.1830] Tn Sovereign Liquidity Hunt v6
- **核心**: 流動性獵殺 (Liquidity Sweep) 與機構位移審計。
- **技術**: Pine Script v6.0 標準, 動態 ATR 風險架構。
- **狀態**: 已實體化至 `strategies/`。

### [v26.0427.1842] Tn Sovereign Optimized Trend v6
- **核心**: 多尺度 EMA 交叉與動態成交量因果過濾。
- **技術**: Pine Script v6.0 標準, ATR 動態風險對位。
- **狀態**: 已實體化至 `strategies/`。

### [v26.0428.0630] Tn Sovereign Lorentzian v6
- **核心**: 洛倫茲分類 (Lorentzian Classification) 與多維特徵因果審計。
- **技術**: Pine Script v6.0 標準, 洛倫茲空間距離度量, 動態風險對位。
- **狀態**: 已實體化至 `strategies/`。
