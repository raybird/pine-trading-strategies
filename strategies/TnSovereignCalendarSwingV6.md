# TnSovereignCalendarSwingV6 — TeleNexus 日曆（星期）擺盪策略

## 概述
移植自 `JoelPasapera/Strategies-in-Pine-Script-v6` 的 `Simple Swing Strategy / Ultra simple strategy.pine`。純以**星期（Day of Week）曆法**驅動的擺盪引擎：於指定進場星期建立方向性倉位，於指定出場星期強制平倉。不參考任何指標，edge 即為「時間編排」本身——日曆季節性累積多日持倉。

## 核心邏輯
- **進場日**（預設 Thursday）：於當日且空倉時開倉（Long 僅在開啟時；Short 另設開關）
- **出場日**（預設 Monday）：抵達當日即平倉所有排程腿
- **防護**：`stable = entryDay != exitDay`，避免進出場日相同造成隔週內反覆
- 進場僅在 `flat`（空倉）時下單一次，不疊加

## 風險管理
- **方向開關**：Long-only / Short-only 獨立啟用
- **ATR Bracket（可選）**：`useBracket` 開啟時，以 `進場均價 ± ATR × 乘數` 附加停損/停利（SL 1.5×、TP 2.0×）
- 固定手數 `lotSize`

## 視覺化
- 出場日背景標記（紅色）；進場日 `CAL-L` / `CAL-S` 三角形；出場日 `CAL-X` 叉號
- 三組 `alertcondition`：排程開多 / 排程開空 / 排程平倉

## 版號
- 版本：v26.0814.1830
- 審計時間：2026-08-14 18:30 CST
- 來源：JoelPasapera/Strategies-in-Pine-Script-v6