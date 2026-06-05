# Tn Sovereign Stoch Divergence v6

**版本**: v26.0605.1830
**來源**: [JoelPasapera/Strategies-in-Pine-Script-v6](https://github.com/JoelPasapera/Strategies-in-Pine-Script-v6) — Stochastic Divergence Strategy

## 核心邏輯

Stochastic %D 背離偵測策略。當價格與 %D 走勢不一致時進場，捕捉趨勢反轉點。

### 信號引擎
- **標準 Stochastic (14,1,3)** — %K 與 %D 雙線隨機指標
- **多頭背離** — 價格更低低點 + %D 更高低點 → 做多
- **空頭背離** — 價格更高高點 + %D 更低高點 → 做空
- **5-bar 樞軸系統** — 自動偵測價格 pivot high/low
- **背離破裂移除** — %D 反向穿越時自動清除已破裂背離線

### 風險管理
- 可選停損（2%）與停利（4%）
- 固定倉位數量

### 視覺化
- 獨立視窗顯示 %K/%D 線
- 超買/超賣水平線（80/20）
- 多空背離虛線連線 + 標籤

## 移植備註
- 原始碼依賴多個陣列管理 pivot 資料，保留完整結構
- 移除冗餘 UI 選項（線條樣式、顏色選擇器），保留核心邏輯