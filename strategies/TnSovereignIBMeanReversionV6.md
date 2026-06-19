# TnSovereignIBMeanReversionV6 — 主權 IB 均值回歸反轉策略

- **移植來源**: Prat617/strategic — IB Mean Reversion Fade (Day-Type Classification)
- **物理時間**: 2026-06-19 18:30 CST | **版本**: v26.0619.1830

## 核心邏輯
1. **IB 形成與日型分類**：09:30-10:30 ET 的 Initial Balance，透過歷史平均範圍分類 (Narrow/Normal/Wide)
2. **日型過濾**：可跳過 Narrow（低波動盤整日）與 Wide（趨勢日），只交易 Normal
3. **延伸區反轉**：價格超出 IB 範圍 0.5-1.0× 後反穿 IB 邊界 (Fade) + MA 濾網
4. **可選均線**：EMA/SMA/VWMA 作為趨勢偏見
5. **停利**：IB 中點或對側邊界；**停損**：0.5×IB Range
6. **日內風控**：最多 1 次每方向、$500 虧損上限、EOD 平倉

## 分類
Mean Reversion & Oscillator（均值回歸與振盪指標）

## 適用市場
NQ/MNQ/ES 期貨（5 分鐘 K 線）
