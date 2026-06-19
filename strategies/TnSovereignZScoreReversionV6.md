# TnSovereignZScoreReversionV6 — TeleNexus 主權 Z-Score 波動率反轉策略

- **移植來源**: Prat617/strategic — Intraday Volatility Reversion Z-Score
- **物理時間**: 2026-06-19 18:30 CST | **版本**: v26.0619.1830

## 核心邏輯
1. **Session VWAP + 標準差**：手動累積 RTH 時段的 TPV/Vol 計算 VWAP 與變異數，推導 Z-Score
2. **耗竭 K 線偵測**：利用 Wick:Body 比 > 2.0 辨識潛在反轉
3. **ATR 百分位體制濾網**：動態計算 ATR 在過去 N 根的百分位排名，高波動時阻擋進場
4. **RSI 極端確認**：75/25 門檻補位耗竭 K 線
5. **目標 VWAP 回歸**：停利設在 VWAP (Z=0)，停損 1.5×ATR
6. **日內風控**：最大日虧損 $500、最多 3 筆交易、EOD 強制平倉

## 分類
Mean Reversion & Oscillator（均值回歸與振盪指標）

## 適用市場
NQ/ES 期貨（5 分鐘 K 線）
