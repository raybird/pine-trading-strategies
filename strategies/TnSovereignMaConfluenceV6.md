# TnSovereignMaConfluenceV6 — TeleNexus 主權移動平均交叉匯流策略

## 概述
移植自 `Viprasol-Tech/pine-script-strategy` 的 `viprasol_ma_cross_strategy.pine`。以**移動平均交叉**為核心（EMA/SMA/WMA/RMA/HMA 五型可選），堆疊 HTF 趨勢、RSI、ADX、成交量、交易時段五大匯流過濾，配雙止損/獲利引擎（ATR 或固定百分比）、ATR 追蹤止損、圖上統計儀表板與完整告警集。

## 核心邏輯

### MA 交叉核心
- 快/慢週期可設（預設 12/26），MA 型態五選一，來源可自訂
- `ta.crossover` 做多、`ta.crossunder` 做空，僅在確認 K 線評估

### 堆疊式匯流過濾（可獨立開關）
- **HTF 趨勢**：`request.security(..., lookahead=barmerge.lookahead_off)` 取高時框 EMA(50)，多單需 `close >= htfEma`
- **RSI**：多單 `RSI >= rsiLong`，空單 `RSI <= rsiShort`
- **ADX**：`adx >= adxMin`
- **成交量**：`volume >= SMA(vol) × volMult`
- **Session**：`inSession` 內才可進場，可選擇收盤強平

## 風險管理
- **Stop/Target 模式**：ATR（SL 2× / TP 3×）或百分比（1.5% / 3.0%），TP 可關閉
- **ATR 追蹤止損**：達活化距離後開始追蹤，只收緊不放大，與固定 SL 取較緊者
- **EOD 強平**：時段結束可全數平倉

## 儀表板與告警
- 2×9 統計表：Position / Net Profit / Win Rate / Profit Factor / Trades / Max Drawdown / Stop-Target / Filters
- 6 組 `alertcondition`：Long / Short / Any Entry / EMA Cross / Position Closed / Session End

## 版號
- 版本：v26.0803.1922
- 審計時間：2026-08-03 19:22 CST
- 來源：Viprasol-Tech/pine-script-strategy
