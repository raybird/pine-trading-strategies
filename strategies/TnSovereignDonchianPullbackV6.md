# TnSovereignDonchianPullbackV6 — TeleNexus Donchian 突破拉回策略

## 概述
移植自 `Ahmed-GoCode/Quant-Edge-Indicators`（MPL-2.0）`Trend & Breakout/Donchian Pullback.pinescript`。不同於直接 chase 突破的傳統 Donchian，此引擎以 **Donchian 通道突破確立趨勢狀態**，等待價格正式**拉回至通道中線 (Midline)** 才建立倉位，並以通道上下緣作為 TP/SL bracket。質押的是「突破後回抽的動量延續」：價格跌破/站上中線而未破壞突破結構，即為多空延續確認。

## 核心邏輯
- **趨勢狀態機**：`low < chanLow` → 熊市；`high > chanHigh` → 牛市（state-based，突破後鎖定）
- **拉回進場**：牛市確立後 `close <= chanMid` 做多；熊市確立後 `close >= chanMid` 做空
- **防重複進場**：`longTaken / shortTaken` Flag 確保每段趨勢腿僅進場一次，平倉後重置
- **Bracket 出場**：TP 預設為對向通道緣（`chanHigh`/`chanLow`），可切換 Fixed R:R 或僅留 Stop

## 風險管理
- 可選 EMA Trend Floor（預設 EMA200）過濾環境
- Session 時段過濾（可選）+ 測試窗時間過濾
- 單一倉位（`pyramiding=0`），權益百分比倉位

## Sovereign Overlays
- Channel High/Low/Midline 視覺 + 通道區填充 + 進場標記
- HUD：趨勢狀態、Midline 距離 %、持倉方向、版號（v26.0819.0630）
- Webhook 就緒 `alertcondition`（多/空拉回觸發）

## 版號
- 版本：v26.0819.0630
- 審計時間：2026-08-19 06:30 CST
- 來源：Ahmed-GoCode/Quant-Edge-Indicators（MPL-2.0）