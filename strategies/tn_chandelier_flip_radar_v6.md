# TeleNexus Sovereign Chandelier Flip Radar V6

> **分類**: Trend & Momentum / Volatility  
> **版號**: v26.0530.1831  
> **獵頭源**: WavesUnchained Chandelier Flip Radar v1.4  
> **狀態**: 已實體化

---

## 策略概述

ATR 追蹤止損策略，具有五層趨勢狀態分類。核心創新在於**趨勢弱化在實際方向改變前即可透過漸進式 K 線著色與可配置警告/危險區域可視化**。此版本加入 TeleNexus 主權因果審計與完整風險管理框架。

## TeleNexus Sovereign 強化

| 項目 | 原始 | 強化後 |
|------|------|--------|
| AI 適應 | K-means 自動選擇乘數 | 主權審計狀態追蹤 + 波動率體感適應 |
| 風險管理 | ATR SL/TP | 可切換 Breakeven / Trailing / Multi-TP |
| 狀態機 | 5 層狀態 | 加入因果審計 (auditEntryPrice/auditEntryBar) |
| 視覺化 | 漸進著色 | 主權 Dashboard + 模式標籤 |

## 核心邏輯

1. **ATR Ratchet Stop** — 多頭 stop 只上移、空頭 stop 只下移
2. **5 層狀態** — Strong / Softening / Warning / Danger / Flip
3. **Body Filter** — 避免 Doji 或 inside-bar 導致偽翻轉
4. **Bull/Bear Trap 偵測** — wick 穿越 flip trigger 但 close 守住
5. **AI K-means** — 自動搜尋最佳 ATR 乘數 (3 clusters)

## 參數建議

| 參數 | 預設 | 說明 |
|------|------|------|
| ATR Period | 30 | 趨勢識別週期 |
| ATR Multiplier | 4.5 | Stop 寬度 |
| Adapt Mode | Off | Off / Simple / AI (K-means) |
| Body Filter | 0.8 ATR | 防止弱翻轉 |
| SL | 1.5 ATR | 停損距離 |
| TP | 3.0 ATR | 止盈距離 |

## 風險

- AI 模式在低 bar count 時收斂不穩定
- 高 ATR Mult 會導致大回撤
- 適合趨勢市場，盤整時偽訊號較多