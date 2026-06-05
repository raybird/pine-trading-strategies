# Tn Sovereign Donchian Breakout v6

**版本**: v26.0605.1830
**來源**: [JoelPasapera/Strategies-in-Pine-Script-v6](https://github.com/JoelPasapera/Strategies-in-Pine-Script-v6) — Donchian Breakout Strategy

## 核心邏輯

時間觸發 + Donchian 通道突破策略。每日特定小時掛 Buy Stop 訂單，突破通道上緣進場，通道下緣離場。

### 信號引擎
- **Donchian 通道 (25)** — 取前 25 根 K 線最高/最低值
- **時間觸發** — 每日指定小時（預設 17:00）掛 Buy Stop 於通道上緣
- **訂單有效期限** — 可設定掛單有效 K 線數（預設 60）
- **通道下緣離場** — 價格回踩通道下緣時停損出場

### 風險管理
- 固定倉位大小
- 通道下緣作為動態停損

### 視覺化
- 通道上下緣線
- 目標時間藍色背景
- 掛單標記（Buy Stop 箭頭）

## 移植備註
- 原始邏輯簡潔，直接移植為 Sovereign 格式
- 保留 time-based entry + Donchian exit 完整雙層結構