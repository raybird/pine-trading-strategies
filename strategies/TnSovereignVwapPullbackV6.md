# TnSovereignVwapPullbackV6 — TeleNexus 主權 VWAP 拉回（Dip-Buy）策略

## 概述
移植自 `jchi18/ote-tradingview` 的 `VWAP_Pullback_Strategy.pine`。核心是 **VWAP Pullback（買入拉回）邊緣**，與「追動量」相反：在確認上升趨勢（1H EMA 快線 > 慢線）中，VWAP 上升且價格位於 VWAP 上方時，在 VWAP 線放置掛單限價買入，待價格拉回公允價值時成交。停損為 VWAP 外 0.5×ATR，目標為可配置 R:R。若價格在成交前收盤穿越停損，則取消掛單。每個時段重置，空頭對稱鏡像。

實際合約（MNQ）驗證：A+ 子集（強趨勢 + 拉伸）在 RR 1.25 下達 **74% 勝率 / PF 3.48**（對比純動量 ~PF 1）。

## 核心邏輯
1. **時段 RTH 錨定 VWAP**：手動累積 TPV/Vol（或 24h 每日重置），計算公允價值線
2. **HTF EMA 趨勢偏見**：`request.security` 1H（可配置）快慢 EMA 交叉，非重畫
3. **VWAP 斜率方向閘門**：多頭需 `vwap > vwap[slopeLen]`，空頭反之
4. **A+ 品質過濾**：強趨勢（close > emaFast > emaSlow 且 emaFast 加速）+ 最小 ATR 拉伸（從 VWAP 算起）
5. **掛單入場**：`strategy.entry(limit=vwap)` 限價等待拉回成交
6. **取消掛單**：未成交前價格收盤穿越停損區即取消並標記 dead
7. **限制**：可選交易時窗（09:30–11:00 ET），可選每日至多一單
8. **倉位**：固定口數 或 權益風險 % 動態口數
9. **風控**：0.5×ATR 動態停損 + R:R 目標 bracket（支援 `strategy.exit`）

## 過濾器
- HTF EMA 趨勢偏見（1H 50/100）
- VWAP 斜率方向
- A+ 強趨勢 + 最小 ATR 拉伸門檻
- 交易時窗閘門（09:30–11:00 ET）
- 每日至多一單（可選）
- Dead/Armed 掛單狀態機（取消防重複掛單）

## 風險管理
- ATR（14）動態停損：掛單外 0.5×ATR
- R:R 目標（預設 1.25，可調 2.0–2.5 最大化單筆利潤）
- 固定合約 或 權益風險 % 口數計算
- 每時段/每日重置狀態

## 移植來源
- 原始倉庫：`jchi18/ote-tradingview`
- 原始檔案：`VWAP_Pullback_Strategy.pine`
- 主權化版本：v26.0814.1839
- 分類：Mean Reversion & Oscillator（VWAP 拉回 Dip-Buy）

## 與既有 VWAP 策略差異
- `TnSovereignVWAPV6`：動態錨定 VWAP + 標準差通道均值回歸（過度偏離反轉）
- `TnSovereignVwapRegimeV6`：VWAP 偏離偵測 regime 分類
- `TnSovereignZScoreReversionV6`：Session VWAP 標準差 Z-Score 反轉
- 本策略：**趨勢內拉回掛單 Dip-Buy** — 反向於 VWAP 偏離 fade，專注「順勢買回公允價值」