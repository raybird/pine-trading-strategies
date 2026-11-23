# TnSovereignDealerGammaDriftV6

> **TeleNexus Sovereign Trading Systems — Pine Script v6**
> Version: `v26.1124.0630` · Causal Audit: `2026-11-24 06:30 CST`

## 策略定位

**Dealer Gamma 避險體制漂移策略**：以 CBOE 波动率期限結構（VIX / VIX3M）
作為造市者「正 gamma Protection」之免付費因果代理。當 `VIX/VIX3M < 0.98`
且 `VIX9D/VIX < 1.05`（無短期波動壓力）時，判定 dealer 處於正 gamma 狀態
——此時 dealer 被迫「買低賣高」吸收波動，午後漂移較易延續。策略僅在
13:00 ET、RTH VWAP 上方進場做多，15:55 ET 強制平倉，屬**微結構／造市者
避險體制**命題，與庫內情緒量表、宏觀事件、指標背離皆不同。

## 與現有庫之差異

- 全庫 `grep -ril "dealer|gamma exposure|kalman" strategies/*.pine` **零命中**。
  既有 `gamma` 字串僅見於 Laguerre 阻尼係數（`TnSovereignLaguerreRsiRegimeV6`）
  與強化學習檔內無關用法，非 dealer hedging 體制。
- `TnSovereignCrowdSentimentConsensusV6` 用的是 CNN 風格 7 組分 Fear &
  Greed 量表；`sentiment_macro_sovereign_v6` 依賴付費 `request.seed()`；
  本策略直接以**波動率期限結構**推論 dealers 的 gamma 暴露方向，資料源
  免費且完全因果（前日已收盤 CBOE 序列）。
- TradingView 同名策略頁（OpenSourceEdge: Shield Battery）受 House Rules
  約束；本移植改以明確 MIT 授權之 GitHub 原始檔為來源。

## 核心邏輯

```
vixRatio   = 前日 CBOE:VIX   / 前日 CBOE:VIX3M
vix9dRatio = 前日 CBOE:VIX9D / 前日 CBOE:VIX

positiveGamma = vixRatio < 0.98      （期限貼水 → dealer 正 gamma）
volStress     = vix9dRatio >= 1.05   （短期恐慌 → 否決）
regimeOk      = positiveGamma and not volStress and 資料可用

RTH VWAP = Σ(typical × volume) / Σvolume，09:30 ET 重置
long = barstate.isconfirmed and 13:00 ET and regimeOk
       and close > RTH VWAP and 每日首次 and 風險距離有效

stop   = 2.0 × ATR15（前根已收盤 15m ATR，最小 16 ticks）
target = 2.5R（選配）；1R 後保本；最長持倉 120 根
exit   = 停損 / 目標 / 持倉上限 / 15:55 ET 強制平倉
```

所有 `request.security` 皆取 `[1]` 前根已收盤值並搭配
`lookahead = barmerge.lookahead_on` 與 `ignore_invalid_symbol = true`；
VIX/VIX3M 缺失時 `regimeOk = false`，fail-closed。

## 主權化改造

| 項目 | 原作者 | 主權版 |
|------|--------|--------|
| 型別 | 自足 v6 `strategy()` | 保留並重構為主權 v6 `strategy()` |
| Gamma 來源 | 前日 VIX/VIX3M proxy + 手動 PRO 覆寫 | 同代理但全數 `ignore_invalid_symbol` + `[1]` 已收盤 + fail-closed；手動覆寫改預設關閉 |
| 事件過濾 | 硬編碼 2024–2026 FOMC 日期表 | **移除日期表**（避免選擇偏見），改 VIX9D 壓力閘門 + 自選事件黑名單 |
| 風控 | ATR15 硬停損、1 合約固定 | ATR15 停損 + 2.5R 目標 + 1R 保本 + 持倉上限 |
| 部位 | 固定 1 口 | 風險距離定倉（0.5% 權益）+ 名目槓桿封頂 2× + `int` 落地 |
| 體制 | 僅 gamma proxy | 另加日線 EMA200 方向閘門 + RVOL + DD |
| 時間紀律 | 13:00 進、15:55 平 | 保留，另加冷卻、時段、1m/5m 圖表閘門 |
| 成交 | `process_orders_on_close=false` | 保留，並要求 `barstate.isconfirmed`；時間平倉 `immediately = true` |
| 通訊 | 文字 alert | JSON Webhook（BUY / ET_FLAT 雙通道） |
| 宣稱 | 「1B+ ticks、32M options rows、Strictly causal」等行銷文字 | 全數移除，僅保留因果儀表板 |

## 非重繪契約

進場與時間出場僅於已收盤 K 棒判定；VIX / VIX3M / VIX9D 取前一根**已收盤**
日線值；ATR15 取前一根**已收盤** 15 分鐘值；日線 EMA 亦取前根收盤值。
所有跨標的序列均帶 `ignore_invalid_symbol = true`。

## 資料合約

- 必要：MNQ/NQ（或流動性指數期貨）OHLC + volume；`CBOE:VIX`、
  `CBOE:VIX3M`（正 gamma 判定）；`CBOE:VIX9D`（壓力否決）。
- 任一 CBOE 序列不可用時策略不進場；與券商回填/合成 K 線無相容保證。

## 來源

移植自 **Open-Source-Edge/everything**（MIT，Copyright 2026 OpenSourceEdge）
`episodes/ep01-dealer-gamma/LongGammaDrift_OpenSource.pine`，branch `main`，
commit `6fb3096ad2db125fb8c537a6a451f780dfcabafb`
（`2026-11-23T02:02:14Z`）。本庫未經獨立回測驗證，不主張任何績效。
