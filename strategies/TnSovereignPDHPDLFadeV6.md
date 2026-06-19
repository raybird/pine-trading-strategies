# TnSovereignPDHPDLFadeV6 — 主權前日高/低均值回歸反轉策略

- **移植來源**: Prat617/strategic — PDH/PDL Mean Reversion Fade
- **物理時間**: 2026-06-19 18:30 CST | **版本**: v26.0619.1830

## 核心邏輯
1. **PDH/PDL 參考**：透過 `request.security` 取得前日日線高/低點
2. **Session VWAP**：RTH 時段 VWAP 作為趨勢偏見濾網
3. **觸及反轉**：價格接觸 PDH (short) 或 PDL (long) 後 + 成交量確認 + VWAP 確認
4. **Swing Stop**：以最近 N 根 K 線的 swing 高/低點作為動態停損
5. **時窗限制**：僅在 09:30-12:30 ET 間交易 (最佳均值回歸時段)
6. **日內風控**：最多 2 筆交易、$500 日虧損上限、EOD 平倉

## 分類
Mean Reversion & Oscillator（均值回歸與振盪指標）

## 適用市場
NQ/ES 期貨（5 分鐘 K 線）
