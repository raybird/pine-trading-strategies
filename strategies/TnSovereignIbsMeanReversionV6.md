# TnSovereignIbsMeanReversionV6

> **TeleNexus Sovereign Trading Systems — Pine Script v6**
> Version: `v26.1118.0630` · Causal Audit: `2026-11-18 06:30 CST`

## 策略定位

**IBS（Internal Bar Strength）均值回歸**：以 `IBS = (close − low)/(high − low)`
衡量收盤在當日區間的位置（0＝收在最低、1＝收在最高）。IBS 偏低代表
賣壓集中的收盤，若能同時滿足「價格低於 N 日高點 − k × 平均真實區間」
之拉回帶，即建立多頭；原作者出場為收盤突破前日高點。

## 與現有庫之差異

- 全庫 `grep -il "ibs" strategies/*.pine` 之既有命中皆為
  `i_ibStartHour`（Initial Balance 時段）或 Fibonacci 之子串，
  **並無以 Internal Bar Strength 為進場主證據者**。
- 既有mean reversion 策略（`TnSovereignZScoreReversionV6`、
  `TnSovereignPDHPDLFadeV6`、`TnSovereignIBMeanReversionV6`、
  `TnSovereignVwapPullbackV6`）分別使用 Z 分數、PDH/PDL、Initial Balance、
  VWAP 公平值；本策略使用**單根 K 棒收盤位置**，屬微觀價格行為維度。

## 核心邏輯

```
ibs      = high > low ? (close − low) / (high − low) : 0.5
rangeAvg = SMA(high − low, 25)
band     = highest(high, 10) − 2.5 × rangeAvg

long  = IBS < 0.30 and close < band
exit  = close > prevDayHigh   (原作者)
      | ATR 硬停損 / 2.5R 目標 / 1R 保本 / 10 根上限  (主權化新增)
```
選配空頭鏡像：`IBS > 0.70 and close > lowest(low,10) + 2.5 × rangeAvg`。
日線 EMA200 同向閘門與 RVOL 閘門預設不同的是刻意保留原策略的
日內均值回歸本質；兩者可依標的開啟。

## 主權化改造

| 項目 | 原作者 | 主權版 |
|------|--------|--------|
| 停損 | 無（僅前日高點出場） | ATR 2.0× 硬停損 + 2.5R 目標 + 1R 保本 + 10 根上限 |
| 部位 | 100% 權益 | 風險距離定倉 + 名目槓桿封頂 + `int` 落地 |
| 時間窗 | `startYear=1990 / endYear=2100` 硬編碼 | 時段 / 每日平倉 / 冷卻 / 持倉上限 |
| 成交 | `process_orders_on_close=true` | `false` + `barstate.isconfirmed`，下一根開盤成交 |
| 體制 | 無 | 日線 EMA200（`lookahead_on` + `ignore_invalid_symbol`） |
| 流動性 | 無 | 選配 RVOL |
| 風控 | 無 | DD 守門 + 冷卻 + 空頭鏡像開關 |
| 宣稱 | 無 | 無（因果儀表板僅呈現狀態） |

## 非重繪契約

所有進場／出場訊號僅於已收盤 K 棒判定；日線序列（EMA、前日高低）
一律取已收盤值並帶 `ignore_invalid_symbol = true`。時間出場使用
`immediately = true` 以貼近原作者「收盤出場」語意。

## 資料合約

- Price：必要（OHLC）。Volume：僅 RVOL 開啟時需要。OI／參考標的：不需要。
- CFD-safe；合成 K 線（Heikin Ashi / Renko）之回測不保證有效。

## 來源

移植自 **Aitradingroom/ai-trading-room**（MIT，Copyright 2026 AI Trading Room）
`strategies/ibs-mean-reversion/ibs_mean_reversion.pine`。
本庫未經獨立回測驗證，不主張任何績效。
