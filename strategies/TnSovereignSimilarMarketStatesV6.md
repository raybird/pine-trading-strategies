# TnSovereignSimilarMarketStatesV6

> **TeleNexus Sovereign Trading Systems — Pine Script v6**
> Version: `v26.1118.0630` · Causal Audit: `2026-11-18 06:30 CST`

## 策略定位

**歷史相似態（Case-Based Reasoning / k-NN Replay）**：在「同一基礎設定」
（EMA 趨勢方向 + 同向動量）的歷史 K 棒中，以四維正規化特徵（RSI、
動量／ATR、EMA 距離／ATR、相對波動率）找 k 個最近鄰；每個鄰居不是用
「原始漲跌幅」代理，而是**以與本筆完全相同的停損距離與持有期重播一筆
歷史交易**，換算成 R 倍數結果。僅當「鄰居均值 − 1×標準誤 > 成本 + 安全
邊際」且有利鄰居比例達標，才放行進場。

## 與現有庫之差異

- 全庫僅 `knn_matrix_ml_v6`、`matrix_knn_ml_v6` 使用 kNN，兩者皆為
  **Lorentzian 距離 + 下一根收盤方向標籤**的靜態分類；本策略為
  **跨案例交易重播 + R 倍數下界 + 成本門檻**之不同命題，非重複覆蓋。
- 全庫 `grep -ril "similar market states\|nearest neighbour" strategies/*.pine`
  僅命中既有 kNN 檔；「歷史類比以真實停損／持有期重播」為全新項目。
- `TnSovereignNeuraRLV6` 雖含 replay 字樣，但其為強化學習軌跡，非
  k-NN 案例檢索與統計下界決策。

## 核心邏輯

### 1. 四維特徵（逐維以自身滾動標準差正規化）
```
rsiFeat    = (RSI(14) − 50) / 50
momFeat    = (close − close[5]) / ATR(14)
trendFeat  = (close − EMA(200)) / ATR(14)
volFeat    = (ATR(14)/close) / SMA(ATR(14)/close, 100)
sd_i       = stdev(feat_i, lookback=1500)
```
正規化避免 EMA 距離（可達數十 ATR）主宰距離、使 RSI 與波動率失語。

### 2. 基礎設定與鄰居取樣
```
trendDir = close > EMA200 and EMA200 > EMA200[5]  ? +1
         : close < EMA200 and EMA200 < EMA200[5]  ? −1 : 0
setupDir = trendDir == +1 and momFeat > 0 ? +1
         : trendDir == −1 and momFeat < 0 ? −1 : 0
```
- 鄰居**只從過去同一 `setupDir` 的 K 棒中抽取**。
- 取樣網格以絕對 `bar_index` 錨定、間隔 ≥ max(spacing, horizon)，
  確保案例結果不重疊；最新案例 `s` 滿足 `s + horizon ≤ bar_index − 1`
  （最晚上一根收盤），**零前視**。
- 距離 = 四維 `log(1 + |Δ|/sd)` 平均；保留距離最小的 k 個。

### 3. 歷史交易重播（本策略核心）
```
entryPx = open[s+1]
stopPx  = close[s] − setupDir × 2.0 × ATR(s)
exitPx  = close[s+horizon]
for k = 1..horizon:
    if setupDir == +1 and low[s+k] ≤ stopPx: exitPx = min(open[s+k], stopPx); break
    if setupDir == −1 and high[s+k] ≥ stopPx: exitPx = max(open[s+k], stopPx); break
outcome = setupDir × (exitPx − entryPx) / (2.0 × ATR(s))   // 單位：R
```
跳空穿越停損時以開價格承接，不給停損價成交之恩惠假設。

### 4. 決策下界
```
expectedR = avg(outcomes)
lowerR    = expectedR − confK × stdev(outcomes) / sqrt(k)
costR     = cost% × close / max(2.0 × ATR, mintick)
pass      = matches == k and lowerR > costR + minEdgeR
            and favorable% ≥ 60%
```
`confK`（預設 1.0）以標準誤折價，避免少數幸運鄰居偽裝成 edge。

## 主權化改造

| 項目 | 原作者 | 主權版 |
|------|--------|--------|
| 成本除零 | `costR` 未保護 ATR=0 | `max(risk, syminfo.mintick)` |
| 最差鄰居索引 | `array.indexof(array.max())` 重複值錯配 | 逐項掃描取得正確索引 |
| 部位 | 固定 10% 權益 | 風險距離定倉 + 名目槓桿封頂 + `int` 落地 |
| 風控 | `strategy.risk.*` 隱性依賴 | 明確 DD / 連虧守門 + 冷卻 + 持倉上限 |
| 體制 | 無 | 日線 EMA50 同向閘門（`lookahead_on` + `ignore_invalid_symbol`） |
| 流動性 | 無 | 選配 RVOL 閘門 |
| 成交對位 | 研究展示表 | 僅保留決策量；`immediately=true` 時間出場 |
| 宣稱 | 成本表 / 隨機基準表 | 全數移除，僅留因果儀表板 |

## 非重繪契約

所有特徵、標準差、鄰居取樣與結果重播僅用已收盤 K 棒；訊號僅於
`barstate.isconfirmed` 判定，訂單於下一根開盤成交
（`process_orders_on_close = false`）。日線序列取已收盤值。

## 資料合約

- Price：必要（OHLC）；Volume：僅 RVOL 開啟時需要；OI／參考標的：不需要。
- CFD-safe；`chart.is_standard` 以外之合成 K 線不保證回測有效。

## 來源

移植自 **casoon/pine-scripts**（MIT，Copyright 2026 WavesUnchained）
`strategies/similar_market_states/similar_market_states_strategy.pine` v1.1.0。
本庫未經獨立回測驗證，不主張任何績效。
