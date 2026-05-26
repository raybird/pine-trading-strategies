# TeleNexus Sovereign Scalping Pro V6

> **分類**: Trend & Momentum / Scalping  
> **版號**: v25.0525.1830  
> **獵頭源**: KEBOSLABS Scalping Pro v3  
> **狀態**: 已實體化

---

## 策略概述

高頻 scalping 策略，從 KEBOSLABS Scalping Pro v3 強化升級。核心創新點為 **4 模式預設風險縮放** (Conservative/Balanced/Aggressive/ULTRA)，可在同一策略框架下適應不同交易風格。

## TeleNexus Sovereign 強化

| 項目 | 原始 | 強化後 |
|------|------|--------|
| 架構 | 扁平化條件堆疊 | 主權因果狀態機 + 4 層過濾管線 |
| 風險管理 | 固定 ATR SL/TP | 波動率體感適應 (volRegime) + 結構停損 |
| 贏率適應 | 內建 winRate 計算 | 加入因果審計追蹤 (auditEntryPrice/auditEntryBar) |
| 時間過濾 | 單一 Session 參數 | 多 Session 複合過濾 + 高波動 Session 增強 |
| 視覺回饋 | 完整 but 雜亂 | 主權 Bias 背景 + 模式專屬配色 |

## 訊號邏輯

1. **CHoCH (變換高低點)** — 60/50/40/28 bars 依模式縮放
2. **BOS (結構突破)** — 突破前高/前低後確認
3. **IDM (誘導獵殺)** — 高/低點掃掠後反轉
4. **濾波器** — RSI、Volume、Trend EMA、ATR、Momentum、Time、ADR
5. **13 項進階優化** — 包含 Kelly 倉位、波動率計時、結構停損、動能反轉退出

## 參數建議

| 參數 | 預設 | 說明 |
|------|------|------|
| ATR Length | 12 | 波動率計算週期 |
| CHoCH Period | 50 | 結構檢測靈敏度 |
| RSI Range | 25-75 | 過濾極端值 |
| Volume Mult | 1.3 | 確認量能放大 |
| Risk:Reward | 1:4 | Balanced 模式 |
| Max Pyramiding | 3 levels | 加倉層數 |

## 風險

- Scalping 策略對交易成本高度敏感 (0.05% commission)
- 高頻在低波動市場易產生假訊號
- ULTRA 模式 max DD 可能 >20%