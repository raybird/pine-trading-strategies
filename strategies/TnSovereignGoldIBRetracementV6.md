# TnSovereignGoldIBRetracementV6 — 主權黃金 IB 突破拉回策略

- **移植來源**: Prat617/strategic — Gold IB Breakout Retracement
- **物理時間**: 2026-06-19 18:30 CST | **版本**: v26.0619.1830

## 核心邏輯
1. **IB (Initial Balance) 形成**：09:30-10:30 ET 計算黃金 GC 期貨的高/低/範圍 %，過濾過窄或過寬的 IB
2. **突破偵測**：價格突破 IB High/Low 後標記方向
3. **拉回入場**：價格回撤至 IB 範圍的 25% 深度 + 成交量放大確認
4. **停利/停損**：TP = IB 極端 + 0.5×IB Range；SL = 進場價 ± 0.6×IB Range
5. **EOD 平倉**：16:00 ET 強制出場

## 分類
Market Structure & Price Action（市場結構與價格行為）

## 適用市場
GC 黃金期貨（5 分鐘 K 線）
