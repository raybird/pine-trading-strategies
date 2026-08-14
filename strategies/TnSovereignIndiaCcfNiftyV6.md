# TnSovereignIndiaCcfNiftyV6 — TeleNexus 印度 NSE 客製匯流期貨（CCF）策略

## 概述
移植自 `jayadevrana/pinescript-custom-confluence-futures-strategy-v6` 的 `pinescript_custom_confluence_futures_strategy_v6.txt`。以 **相對強度（Relative Strength）** 為軸心，融合 SuperTrend、雙 EMA 交叉、MACD、RSI、ADX 與量能 EMA 的多層匯流引擎，針對印度 NSE 期貨/選擇權（NIFTY）設計，採 50/50 兩段式金字塔進場，並以選擇權 OI 確認（條件 9）與模擬 ATM CE/PE 對沖訊號收尾。

## 核心邏輯

### 相對強度（RS）引擎
- `f_rs(_src, _bench, _len)`：以 `_src / _src[_len]` 相對 `_benchmark / _benchmark[_len]` 之比值減 1 得出 RS，跨零軸為多空訊號
- **RS 21**（零軸方向）為核心條件之一；**RS 55** 為進場階梯閘門（第二腿）
- `strictRs` 開啟時，要求 RS 21 與 RS 55 於同根 K 線同步穿越零軸

### 多空核心條件（Buy / Sell Core）
- **C1 ADX**：`adxValue > 閾值` 且正在上升（`adxValue > adxValue[1]`）
- **C2 EMA 交叉**：快 EMA（預設 3）> 慢 EMA（預設 13）
- **C3 MACD**：MACD 線 > 訊號線 且 MACD 線 > 0
- **C4 RSI**：RSI > 50（多）
- **C5 RS 21**、**C6 RS 55**：均須跨零軸同向
- **C8 Volume**：`volume > Volume EMA`
- **C9 選擇權/OI 確認**（可選）：期貨 OI 上升 + CE OI 下降 + PE OI 上升（做多側）

### 兩段式進場（50 / 50）
- **Full Setup**：Core + RS55 成立 → 同時掛 `LONG-1` / `LONG-2`（或 `SHORT-1`/`SHORT-2`）各 50%
- **Half Setup**：Core 成立但 RS55 未過 → 僅掛第一腿 50%，等待 RS55
- **Add Setup**：持倉中 RS55 補足 → 掛第二腿 50%（狀態由 `longLeg1/longLeg2` 旗標隔離）

### 出場
- **Half Exit**：EMA + MACD 反向翻轉 → 平第一腿
- **Full Exit**：EMA + MACD + RSI + 穿越趨勢 EMA + Heikin-Ashi 實心 K 線確認 → 全平
- **Gap-Through Stop**（可選）：收盤跌破/突破進場均價 ± 停損 %，於當根收盤強制平倉

### CE / PE 對沖與背離
- **背離引擎**：期貨創新高/新低 而 CE/PE 未同步創高/創低 → `longSideDivergence` / `shortSideDivergence`
- 配合 CE/PE 的 Heikin-Ashi 轉折（`ceSolidRed` / `peSolidGreen` 等）觸發 `Sell CE / Buy PE / Sell PE / Buy CE` 對沖訊號
- `simHedge` 開啟時以 `strategy.order` 於圖表標的模擬對沖腿（真實下單僅能於 CE/PE 自身標的）

## 風控與執行
- **Pyramiding**：最多 4 筆；`default_qty_type = percent_of_equity`（50%）、滑價 1、佣金 0.02%
- `process_orders_on_close = true` + `calc_on_order_fills = true`
- 所有進入/出場/對沖皆輸出 `alertcondition` 供 webhook 串接 MT5 等下游執行

## 版號
- 版本：v26.0814.1830
- 審計時間：2026-08-14 18:30 CST
- 來源：jayadevrana/pinescript-custom-confluence-futures-strategy-v6
