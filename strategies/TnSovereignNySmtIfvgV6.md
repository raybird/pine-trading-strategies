# TnSovereignNySmtIfvgV6

> **TeleNexus Sovereign Trading Systems — Pine Script v6**
> Version: `v26.1020.1830` · Causal Audit: `2026-10-20 18:30 CST`

## 策略定位

**NY 股市 Killzone 時段的 ICT 三段式 set-up 移植**：HTF 偏見（收線確認的
EMA + 結構 / HTF K 線實體，可切換）＋ 盤中 VWAP 對齊 → 跨資產 **SMT
Divergence** 武裝 → 近期 FVG 被位移 K 線反轉後的 **IFVG 回測（retrace）**
觸及才進場。僅在 NY Killzone（預設 09:35–11:00 ET，刻意避開 09:30 Judas
swing）與可選 London Killzone 開單，每 session 限 1 筆，15:55 ET 前強制
flatten。

## 與現有庫之差異

全庫 `SMT` 覆蓋數 = **0**（`grep -ril "SMT" *.pine` 零命中）。現有 ICT 系
（`TnSovereignIctLsReversalV6` 等）做的是**單一標的的** sweep → displacement
→ MSS → FVG 執行；`TnSovereignZoneFlowV6` / `TnSovereignMatrixSovereignV6`
做的是體制/矩陣評分。**跨資產（EURUSD↔GBPUSD、NQ↔ES、BTC↔ETH）的轉嫁
背離（SMT）作為必要進場武裝，本策略為庫內首例**，且搭配 IFVG 反轉回測
入場（而非 FVG 直接入場），填補「SMT 武裝 + IFVG 反轉回測 + 時段紀律」
三者合體的紀律缺口。

## 核心邏輯

### 1. 時段紀律（Killzone + 每日限單）
- `NY Killzone` 預設 `0935-1100`（美國東岸），`London Killzone` 可選
  `0230-0500`；`NY Active Session 0930-1555` 為收盤平倉邊界。
- `isNewSession` 以 session 起點沿 (`not inFullSession[1]`) 重置
  `tradesToday`；`maxTradesPerDay` 預設 1（上限 5）。
- `flattenEod` 在非活躍 session 且仍有持倉時 `strategy.close_all()`。

### 2. HTF 偏見（非重繪契約）
```
[htfClose, htfOpen, htfEma, htfPrevHigh, htfPrevLow] =
    request.security(syminfo.tickerid, htfTf, [close[1], open[1], ema[1],
                      htfSwingHigh[2], htfSwingLow[2]], lookahead=lookahead_on)
```
取**已收盤之 HTF 序列**（`[1]` / `[2]` 滯後 + `lookahead_on` = 等同
confirmed-bar 且無前視偏差）。四種模式：`EMA + Structure`（收在 EMA 同側且
未破 HTF 前低/前高）/ `EMA Only` / `HTF Candle Close` / `Unfiltered`。

### 3. SMT Divergence 引擎
- `ta.pivothigh / ta.pivotlow` 左右各 `smtPivotLen`（預設 3）→ 樞軸**右側
  確認後才成立**（非重繪）。
- 主標的掃低（或相關標的掃低）＋ 對手守住 ＋ **陽線收線** → Bullish SMT；
  鏡像為 Bearish SMT。
- SMT 標籤僅在 entry window 內繪製，訊號以 `smtValidBars`（預設 25 bars）
  有效窗武裝 `smtBullActive / smtBearActive`；`useSmt=false` 可旁路。

### 4. FVG → 反轉（IFVG）→ 回測入場
- **FVG 偵測**：需 `gapWidth >= atr(14) * fvgMinAtrMult`（預設 0.15）且
  中間 K 線為趨勢 K（`close[1] < open[1]` 等），過濾微噪缺口。
- **反轉確認**：收盤穿越對向 FVG 邊界 **且** `bodyRatio >= dispBodyRatio`
  （預設 0.45）位移 K 線，才建立 IFVG 區間。
- **失效**：`ifvgMaxWaitBars`（預設 15）逾時，或收盤退回對向邊界外。
- **回測入場**：`bar_index > ifvgBar`（**不追當根反轉**）＋ 觸及
  Top/Bottom Edge 或 50% CE ＋ 收盤仍在區間內 → `bullRetraceHit` /
  `bearRetraceHit`。

### 5. 風險管理與出場
| 機制 | 說明 |
|------|------|
| **停損** | `min(IFVG 另一邊界, 5 根內 swing)` ± `slBufferAtr × ATR`；風險下限 `0.5×ATR` |
| **最終目標** | `1:2 R:R` / `1:3 R:R` / 靜止流動性（`liqLookback` 最高/最低 ± 0.15 ATR 緩衝，夾在 1.5R–3R） |
| **TP1 部份停利** | 預設 `1R` 出 60%，隨後 SL 移至 `+0.05R` 保本偏移（保本出場亦計為贏單） |
| **槓桿** | `leverageMult`（預設 15×，`equity × 15 / close` 計算部位） |
| **紀律** | `pyramiding=0` 單一持倉、每 session 限單、`calc_on_every_tick=false` |

### 6. 視覺與儀表
Killzone 背景、Session VWAP、Active SL/TP1/TP2 線、IFVG box、SMT+/SMT-
標籤；右上 2×7 Dashboard 顯示 session 狀態、HTF 偏見、SMT 狀態、IFVG 區、
Win Rate、Profit Factor、Leverage。

## 參數表

| 群組 | 參數 | 說明 | 預設 |
|------|------|------|------|
| 1. Session | NY Killzone Entry Window | NY 開單時段（ET） | 0935-1100 |
| 1. Session | London Killzone | 是否併用倫敦開盤 | false |
| 1. Session | NY Active Session | 收盤強制平倉邊界 | 0930-1555 |
| 1. Session | Session Timezone | America/New_York / UTC / Europe/London | America/New_York |
| 1. Session | Max Trades Per Session | 每 session 限單數 | 1 |
| 1. Session | Flatten Positions at Session Close | 收盤平倉 | true |
| 2. HTF | Higher Timeframe (Bias) | 偏見時框 | 60 |
| 2. HTF | HTF Bias Determination | 4 種偏見模式 | EMA + Structure |
| 2. HTF | HTF Institutional EMA Length | HTF EMA | 20 |
| 2. HTF | Require Intraday VWAP Alignment | 多須 ≥VWAP、空須 ≤VWAP | true |
| 3. SMT | Require SMT Divergence Confirmation | SMT 武裝開關 | true |
| 3. SMT | Correlated SMT Symbol | 相關標的（GBPUSD/ES1!/ETHUSDT） | FX:GBPUSD |
| 3. SMT | SMT Swing Pivot Lookback | 樞軸左右窗 | 3 |
| 3. SMT | SMT Signal Validity Window | SMT 有效 bars | 25 |
| 4. IFVG | Min FVG Gap Width (ATR Mult) | 最小缺口寬度 | 0.15 |
| 4. IFVG | Min Inversion Candle Body % | 反轉位移實體比 | 0.45 |
| 4. IFVG | Max Bars to Wait for Retrace | 回測逾時 | 15 |
| 4. IFVG | Retrace Entry Depth | 邊界 / 50% CE | IFVG Top/Bottom Edge |
| 5. Risk | Account Leverage Multiplier | 帳戶槓桿倍率 | 15.0 |
| 5. Risk | Runner Target Mode | 1:2 / 1:3 / 靜止流動性 | 1:2 R:R |
| 5. Risk | Resting Liquidity Lookback | 流動性回看 bars | 40 |
| 5. Risk | Liquidity Front-Run Buffer (ATR) | 提前掛單緩衝 | 0.15 |
| 5. Risk | Enable Partial TP1 + Breakeven Lock | TP1 部停 + 保本鎖 | true |
| 5. Risk | TP1 R:R / TP1 Close % / BE Offset | 1R / 60% / +0.05R | 1.0 / 60.0 / 0.05 |
| 5. Risk | Stop Loss Buffer (ATR) | 停損緩衝 | 0.25 |
| 6. Visuals | IFVG Zones / SMT Labels / Dashboard | 三組視覺開關 | true |

## 異動記錄

- **v26.1020.1830** — 獵頭審計 #145：GitHub 新出現倉庫 **Rakeshks7/ict-ny-smt-ifvg-pine-v6**
  （**MIT**，2026-10-18 建立，2026-10-18 推送）之 `NY Open ICT: HTF Bias +
  SMT + IFVG Retrace (Pine v6)`（379 行 v6 `strategy()` 自足，僅 2 個
  `request.security`、無外部 lib）。全庫 SMT 覆蓋數 = 0，判定為全新合格
  實體；移除其宣稱之勝率/績效字串並加掛主權版號與非重繪註記，保留原始
  邏輯，改名為 `TnSovereignNySmtIfvgV6`，歸 **Market Structure & Price
  Action 38→39**。

## 聲明

*執行主權，因果必達。本策略由 MIT 授權來源主權化重寫，非金融投資建議，
請自行回測驗證。原作者宣稱之 75% 勝率 / 4.17 PF 為其個人回測結果，不構成本系統之績效保證。*
