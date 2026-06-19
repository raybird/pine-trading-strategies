# TnSovereignIBVWAPConfluenceV6 — 主權 IB+VWAP 匯流策略

- **移植來源**: Prat617/strategic — IB + VWAP Confluence (Ultimate Combo)
- **物理時間**: 2026-06-19 18:30 CST | **版本**: v26.0619.1830

## 核心邏輯
1. **IB (Initial Balance) 形成**：09:30-10:30 ET 高/低/中點，搭配歷史平均範圍分類 Narrow/Medium/Wide
2. **Session VWAP**：手動累積 RTH 時段 TPV/Vol
3. **拒絕 K 線偵測**：Wick:Body 比 > 1.5 信號 + 成交量萎縮 = Smart Money 不推動
4. **品質評分系統 (0-10)**：IB 寬度 + 延伸區 + 拒絕 K 線 + VWAP 接近度 + 成交量萎縮 + R:R 檢查 + 最佳時窗 = 分數決定口數 (1-3 口)
5. **停利**：IB 中點或 VWAP (取近者)；**停損**：0.5×IB Range
6. **日內風控**：最大日虧損 $500、EOD 強制平倉

## 分類
Market Structure & Price Action（市場結構與價格行為）

## 適用市場
NQ/MNQ 期貨（5 分鐘 K 線）
