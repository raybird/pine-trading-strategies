# TeleNexus Sovereign Adaptive Risk Regime V6

> **分類**: Volatility & Breakout  
> **版號**: v25.0525.1830  
> **獵頭源**: PineGen-AI Adaptive Risk Regime Strategy  
> **狀態**: 已實體化

---

## 策略概述

波動率體感轉換策略。偵測市場狀態（極低/低/中/高/極高波動），自動切換均值回歸與趨勢突破模式。這是 PineGen-AI 系列中邏輯最簡潔但概念最強的策略之一。

## TeleNexus Sovereign 強化

| 項目 | 原始 | 強化後 |
|------|------|--------|
| 波動偵測 | 單一 ATR vs SMA | 雙 ATR (14+28) + 斜率 + 5 級狀態機 |
| 均值回歸 | 單純 range 上下 | + RSI 極端值確認 (35/65) |
| 突破確認 | 無 | + 波動趨勢方向確認 (volTrend) |
| 風險管理 | 固定 ATR 多倍 | 狀態相關動態 SL/TP 帶 (5 級縮放) |
| 審計追蹤 | 無 | 完整 causal audit (entry/bar/regime/reason) |

## 訊號邏輯

### 狀態機定義

| 狀態 | ATR Ratio | 行為 |
|------|-----------|------|
| Extreme Low | <0.6 | 緊 rang, tight SL |
| Low | <0.85 | 均值回歸優先 |
| Medium | <1.15 | 混合模式 (方向由 ATR 趨勢決定) |
| High | <1.5 | 突破交易優先 |
| Extreme High | ≥1.5 | 寬停損追趨勢 |

### 進場條件

- **低波動**: 價格觸及 range 極限 + RSI 超買/超賣 + 均值回歸
- **高波動**: 價格突破 range + ATR 斜率上升 (long) / 下降 (short)
- **中波動**: 突破方向由 ATR 快/慢線決定

## 參數建議

| 參數 | 預設 | 說明 |
|------|------|------|
| ATR Fast | 14 | 短週期波動 |
| ATR Slow | 28 | 長週期波動基準 |
| Vol Lookback | 50 | 波動率均線週期 |
| Range Len | 20 | 區間計算長度 |
| Risk:Reward | 1:2 | 固定 R:R |
| ATR Stop Mult | 1.5 | 停損倍數基線 |

## 風險

- 在極低波動轉高波動的過渡期可能產生假訊號
- 狀態機切換有 1 bar 延遲