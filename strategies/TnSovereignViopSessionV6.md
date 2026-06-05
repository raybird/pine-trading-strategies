# Tn Sovereign VIOP Session v6

**版本**: v26.0605.1830
**來源**: [trugurpala/pinescriptv6](https://github.com/trugurpala/pinescriptv6) — VIOP Session Strategy

## 核心邏輯

時段規訓 + EMA 交叉 + ATR 風控的簡潔型策略，專為土耳其 VİOP 期貨市場（BIST30）設計。

### 信號引擎
- **EMA 9/21 交叉** — 快慢線金叉/死叉作為主要進場訊號
- **時段過濾** — 僅在 09:30–18:15 UTC+3 交易時段內產生訊號
- **收盤強制平倉** — 時段結束自動關閉所有持倉

### 風險管理
- ATR 倍數停損（2×ATR）與停利（3×ATR）
- 可選「僅做多」模式（longOnly）

### 視覺化
- 時段內藍色背景、時段外灰色背景
- EMA 多空方向著色
- 多空訊號三角標記

## 移植備註
- 原始碼無相依外部函式庫，直接移植為 TeleNexus Sovereign 格式
- 移除 Turkish locale 註解，保留實質邏輯