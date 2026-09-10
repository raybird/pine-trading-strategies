# TnSovereignReversalScoreV6 — TeleNexus 反轉引擎評分主權策略

> **分類**: Market Structure & Price Action / Reversal  
> **版號**: v26.0910.1830  
> **獵頭源**: casoon/pine-scripts (WavesUnchained) Reversal Engine Score v1.6.1  
> **狀態**: 已實體化

---

## 策略概述

專注「流動性掃蕩反轉」的**逐級評分斜坡**系統。與既有的 `TnSovereignReversalEngineV6`（分形熵合併版）不同，本版本保留 Reversal Engine Score 的 **Score A→H 階梯**：每次通過一道硬關卡（Sweep → Corridor → HTF Trend → Structure → Wave-Trend）評分即升一級，最後以最低入場等級（預設 G）與 **EMA 退火 capacitor**（防連續過度交易）確認進場。

## TeleNexus Sovereign 強化

| 項目 | 原始 | 強化後 |
|------|------|--------|
| 評分 | Score A→H | 加 `minEntryGrade` 可調門檻 + Quality Cap |
| Sweep | 穿越再回收 | Relational Sweep（影線穿越 + 收盤回收 + 可加 buffer） |
| Capacitor | 固定計數 | EMA 退火充電（`capLen` 平順，回充後才允再出手） |
| 風控 | 0.75R/1.5R | bracket + ATR corridor + Trailing + 1-R loss barrier |

## 核心邏輯

1. **Liquidity Sweep** — `low ≤ swingLow(buffer)` 後收盤回收 → 開啟多候選窗（空方對稱）
2. **ATR Corridor** — ATR 落入常態帶（排除壓縮噪音 / 過度尖峰）
3. **HTF EMA** — 200 慢線全球地 + 50 快線方向
4. **BOS Structure** — pivot 突破後 `close` 確認結構方向
5. **Wave-Trend** — MOM 9×12 + SMA4 平滑動量對位
6. **Score Ladder** — 每關 +1 級，達 `minEntryGrade` 且 capacitor 就緒 → 入場

## 參數建議

| 參數 | 預設 | 說明 |
|------|------|------|
| Sweep Swing Length | 10 | 掃蕩樞軸窗口 |
| ATR Corridor | 0.5 / 3.5 | 常態帶上下界 |
| Min Entry Grade | G | E/F/G/H 可選 |
| Capacitor Length | 9 | 退火充電平順 |
| SL / TP | 60 / 120 | 1:2 bracket |

## 風險

- 多道硬關卡使訊號頻率低（高階 G/H 稀少）
- 強趨勢下「逆勢反轉」仍虧損，BOS 方向需與 HTF 對位
- Capacitor 機制會延遲快速連續反轉的二次進場