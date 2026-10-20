# TnSovereignCommodityPulseMatrixV6

> **TeleNexus Sovereign Trading Systems — Pine Script v6**
> Version: `v26.1020.1830` · Causal Audit: `2026-10-20 18:30 CST`

## 策略定位

**商品／期貨的六類別多時框評分引擎**：把資金流（Flow）、動量（Momentum）、
趨勢（Trend）、波動（Volatility）、結構（Structure）、背離（Divergence）
六個 -1..+1 標準化評分，跨 TF1/TF2/TF3/圖表時框融合為總分與 0..1 的
**Heat Score**（setup 品質）。入場走三家族（Breakout / Pullback /
Continuation）→ 訊號品質閘門（ATR + 成交量）→ 證據計數 Final Gate →
`finalLong / finalShort`，以 ATR 停損與 TP1/TP2/TP3 三段獲利了結。

## 與現有庫之差異

庫內已有印度 NSE 期貨匯流（`TnSovereignIndiaCcfNiftyV6`，RS + 匯流）與
多因子評分（`tn_multi_factor_sovereign_v6`），但**沒有一支把商品/期貨的
六類別 × 多時框標準化評分矩陣作為單一可審計總線**，也沒有 Heat Score /
Diamond Zones / A-Setup 分級 / Early Reversal 候選這一整套「setup 成熟度
語境圖層」。`TnSovereignMatrixSovereignV6` 是 ICT 矩陣而非跨類別統計評分；
`TnSovereignZoneFlowV6` 是體制計分。本策略填補**「商品期貨 × 六類別
多時框評分 × setup 品質分級」**缺口。

## 核心邏輯

### 1. 六類別 × 多時框評分
- `request.security(syminfo.tickerid, timeframe, calculateEssentialIndicators(close),
  lookahead=barmerge.lookahead_off, gaps=barmerge.gaps_off)` — 以 **UDF
  回傳 struct** 取一次即得各時框指標，`MultiTimeframeScores` 彙整
  TF1/TF2/TF3；**若圖表時框與其中一格相同即重用該分數、不重複呼叫**
  （記憶體優化，全檔僅 1 個 `request.security` 調用點）。
- `calculateAggregateScore` 依可配置權重融合六類分數；`getCategoryConsensus`
  檢查單一類別跨時框共識。**Volume 缺失時 Flow 類別權重被剔除並重新
  正規化**（資料契約降級，不假造成交資料）。

### 2. Heat Score（setup 品質 0..1）
`heatScore = pow(heatScoreRaw, 1.2)`；入場強度分解中 **Heat 佔 25% 權重**。
`entryHeatMin`（預設 0.40）為 Final Signal Gate 的**證據點之一（非否決權）**；
`earlyMinHeat`（0.25）門檻刻意低於正式入場，作為資訊層。

### 3. 入場引擎 V2（三家族 + 狀態機）
| 家族 | 觸發 |
|------|------|
| **Breakout** | `detectBreakout` — 突破關鍵位且帶動量確認 |
| **Pullback** | `detectPullback` — 拉回到支撐/阻力區（`nearSupport`/`nearResistance`）＋ JMA50 趨勢偏向 |
| **Continuation** | `detectContinuation` — 迷你拉回後的趨勢延續 |

`entryDensity`（Few / Moderate / Many）調整訊號密度；`allowCounterTrendEntries`
預設 **false**（逆勢入場需 1.5× 更強動量）；`useTrendFilter` 預設 **false**
（趨勢語境已由入場強度與 Heat 評分表示）。
`processEntry` / `updateEntryStateMachine` 以 **bar 收線確認的 fresh
trigger + entryCooldown + upgradeDelta** 去重，避免同向重複觸發。

### 4. 訊號品質閘門與 Final Gate
```
finalLong  = triggerLong  and not qualityVeto and trendOkLong
             and longEvidence  >= evidenceThreshold
```
- **Quality Gate**（`useQualityGate`）：`ATR/ATR_SMA`（0.8 收縮 / 1.2 擴張）
  與 `Vol/Vol_SMA`（0.7 低量 / 1.2 高量）；可設定低量擋入場、收縮區禁止
  趨勢訊號、但**允許區間內靠支撐阻力的均值回歸訊號**。
- **Signal Boost**：RSI `<25/>75` 外緣與 WaveTrend 外緣各可加成
  +0.15 / +0.10 強度。
- **Final Signal Gate**：`finalMinGate`（預設 4，2–5）證據計數嚴格度 +
  `strengthThreshold`（0.55）強度下限。
- **A-Setup**：`heat ≥ 0.65` 且 `strength ≥ 0.70` 且 `isTrending` 且
  `close > JMA50 > JMA20` 的高品質訊號標記。

### 5. 語境圖層（刻意不混入訊號）
- **Early Reversal Candidates** — `showEarlyReversal`，需 JMA20 收復/拒守 ＋
  可選背離區 / 耗竭 / 外緣證據，資訊層非進場。
- **Diamond Zones** — 支撐阻力盒，作為停損語境。
- **Confirmed Swing Layer** — `pivotLeft=10 / pivotRight=8` ＋嚴格樞軸
  確認（`revStrictWindow=100` bar 絕對外緣）＋最小擺動幅度
  （`revMinSwingATR=1.5`），僅圖形標記。

### 6. 風險管理與出場
| 機制 | 說明 |
|------|------|
| **停損** | `SL = ATR × atrSLmult`（預設 1.5），併入 VolStop（`volStopATRMult` 2.0）語境 |
| **停利** | `TP1 = ATR×1.0`、`TP2 = ATR×1.5`、`TP3 = ATR×2.0`；`exitLvlInput` 選擇實際執行層 |
| **保本** | `enableBE` + `beATRInput`（預設 1.0×ATR 觸發），**併入單一 stop level**（`strategy.exit` 只掛一檔 stop，避免 exit 競態） |
| **紀律** | `pyramiding=0`、`cooldownBars`、`confirmClose`（僅收線進場）、`alertsOnBarClose` |
| **風控濾網** | Session 日期區間、Max Drawdown 20%、Max Intraday Loss 5%、Max Consecutive Losses 5（皆預設關） |
| **帳戶設定** | `percent_of_equity 10%`、手續費 2%、滑價 1 tick、`max_bars_back=500` |

### 7. 資料契約
- **Price**：必要（圖表 symbol，無 `input.symbol` 輸入）
- **Volume**：可選 — 僅接受真實成交數量（MFI/OBV/VFI/VWAP 匯流），tick /
  n/a 時**降級為中性分數**（不偽造 0 或 1）
- **OI / 參考資料**：不需要
- **合成 K 線**（Heikin Ashi / Renko）：右下角常駐紅字警示「回測無效」

## 參數表（節錄）

| 群組 | 參數 | 說明 | 預設 |
|------|------|------|------|
| Entry Engine | Signal Density | Few / Moderate / Many | Moderate |
| Entry Engine | Breakout / Pullback / Continuation | 三家族獨立開關 | true |
| Entry Engine | Allow Counter-Trend Entries | 逆勢入場（需 1.5× 動量） | false |
| Entry Engine | Trend Filter (regime + JMA50) | 硬趨勢濾網 | false |
| Entry Engine | VolStop ATR Multiplier | 波動停損倍率 | 2.0 |
| Entry Engine | Trend JMA Fast / Slow | 趨勢偏向 JMA | 50 / 100 |
| Signal Boost | RSI Extreme Boost / Threshold / Amount | RSI 外緣加成 | true / 25.0 / 0.15 |
| Signal Boost | WaveTrend Extreme Boost / Threshold / Amount | WT 外緣加成 | true / 60.0 / 0.10 |
| Signal Boost | Strength Threshold | 最終訊號強度下限 | 0.55 |
| Signal Boost | Entry Heat Evidence (min) | Final Gate 證據點 heat 門檻 | 0.40 |
| Signal Boost | Final Signal Gate (strictness) | 證據計數嚴格度 2–5 | 4 |
| Signal Quality | Enable Quality Gate | ATR + 成交量品質濾網 | false |
| Signal Quality | ATR Contract / Expand Threshold | 0.8 / 1.2 | 0.8 / 1.2 |
| Signal Quality | Volume Low / High Threshold | 0.7 / 1.2 | 0.7 / 1.2 |
| Early Reversal | Require JMA20 / Divergence / Exhaustion / Extremes | 四證據獨立開關 | true |
| Early Reversal | Early Min Heat / Cooldown | 0.25 / 8 bars | 0.25 / 8 |
| Confirmed Swing | Pivot Left / Right / Strict Window / Min Swing ATR | 樞軸語境圖層 | 10 / 8 / 100 / 1.5 |
| Technical | Stop-Loss = ATR × | 停損倍率 | 1.5 |
| Take-Profit | TP1 / TP2 / TP3 ATR × | 三段停利 | 1.0 / 1.5 / 2.0 |
| Strategy | Trade Direction / Confirm Close / Cooldown / Break-Even | 紀律開關 | Both / true / 0 / false |
| Filters | Session / Date Range / Max DD / Max Intraday DD / Loss Streak | 風控濾網（皆預設關） | — |
| Alerts | Alerts only on bar close | 僅收線警示 | true |

## 異動記錄

- **v26.1020.1830** — 獵頭審計 #145：GitHub commits API 全域掃描
  （`extension:pine committer-date:>2026-10-05`）出線 **casoon/pine-scripts**
  於 2026-10-12 提交之 `strategies/commodity_pulse_matrix/
  commodity_pulse_matrix_v4_strategy.pine`（**MIT**，5,502 行、242 KB、
  `//@version=6`、單一 `strategy()` 宣告、僅 1 個 `request.security` 呼叫
  點、無外部 `import`／無 `input.symbol`，括號完全配對）。#138 首度覆蓋
  casoon 時該檔尚未存在，且全庫無 commodity pulse / 六類別評分矩陣；
  移植主權版號與資料契約註記，保留原邏輯，改名為
  `TnSovereignCommodityPulseMatrixV6`，歸 **Trend & Momentum 22→23**。

## 聲明

*執行主權，因果必達。本策略由 MIT 授權來源主權化重寫，非金融投資建議，
請自行回測驗證；商品/期貨類標的請確認所用數據具備真實成交量，否則 Flow
類別將自動降級。*
