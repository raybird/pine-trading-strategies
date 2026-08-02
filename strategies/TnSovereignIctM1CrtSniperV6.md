# TnSovereignIctM1CrtSniperV6 — TeleNexus 主權 ICT/SMC M1 狙擊策略（CRT + Structure + PI）

## 概述
移植自 `thesenegalesehitch/Pine-Script` 的 `ict-smc-sniper.pine`（ICT/SMC M1 Sniper | CRT + Structure + PI，作者 Alexandre Albert Ndour）。以「CRT（Candle Range Theory）+ M15 結構 + PI 價格利益引擎」三階段構築 M1 狙擊系統，每一層獨立確認後才允許觸發。

## 核心邏輯

### 階段 1 — H1 CRT（Candle Range Theory）
- 確認 H1 收線完全落在前一根 H1 範圍內（內部 K 線）
- 多頭 CRT：上緣前高 + 目標延伸 `範圍 × 1`
- 空頭 CRT：下緣前低 + 目標延伸 `範圍 × 1`
- CRT 範圍同時作為 Premium/Discount 分區基準

### 階段 2 — M15 結構與擺動（BOS/CHOCH）
- `ta.pivothigh/low` 偵測 M15 擺動高/低
- 在 CRT 有效前提下，收線突破擺動高 → BULL；跌破擺動低 → BEAR
- 提供買/賣方方向偏見

### 階段 3 — PI 引擎（Price Interest）
- **FVG**：多頭/空頭失衡區（兩根連續同向 K 線 + 最小 Pips 門檻）
- **Order Block**：以位移 K 線（impulse）為基礎構建
- 未接合（unmitigated）偵測：價格穿越後標記為灰化失效
- 入場必須位於未接合的 FVG 或 OB 區間內

## 入場邏輯
- **BUY**：CRT 多頭 + M15 BULL + Discount 區 + 未接合多頭 PI + 多頭位移 + 波動率過濾 + 時段
- **SELL**：CRT 空頭 + M15 BEAR + Premium 區 + 未接合空頭 PI + 空頭位移 + 波動率過濾 + 時段

## 風險管理
- 停損：CRT 範圍邊界（或 ATR 備援）
- 獲利目標：停損距離 × R:R
- **Break Even**：1R 或 Sweep 觸發後移動至成本價
- 時段門控：倫敦（08:00–12:00）與紐約（13:00–17:00）可獨立開關

## 移植來源
- 原始倉庫：`thesenegalesehitch/Pine-Script`
- 原始檔案：`pine-scripts/strategies/ict-smc-sniper.pine`
- 主權化版本：v26.0802.1830
