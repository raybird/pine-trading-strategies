# TnSovereignHFTEngineV6 — TeleNexus 機構級 HFT 機率評分引擎

**版本**: v26.0604.1830 | **移植自**: QuantAlgo institutional-hft-engine

## 核心邏輯
HFT 機率評分系統（0-100），整合 SMC 結構 + 動量 + 區間脈絡 + 流動性獵取的加權評分。僅在分數超過動態閾值時進場。

## 主要功能
- **機率評分引擎**: 多維度評分（結構品質 25pt、趨勢排列 10pt、動量擴張 15pt、流動性掃除 25pt、CHOCH/BOS 20pt、OB/FVG 15pt、價格離散 10pt）
- **自適應閾值**: 根據市場體質（盤整+15、高波動+10、強趨勢-10），範圍 40-95
- **機構風控**: 日虧限額、動態風險縮放、連損暫停、冷卻機制
- **HFT 執行**: 雙 TP（1.5R / 3.0R）、Break-Even 保護、波動率追蹤移動停損

## 參數
- Base Risk Per Trade: 1.0%
- Max Daily Drawdown: 4.0%
- Max Consec Losses: 3
- Cooldown Bars: 5
- Strict Mode: HTF 偏向校準
- Killzones Only: 倫敦/紐約時段

## Dashboard
即時顯示：Status、Daily DD、Regime、Macro Bias、Threshold、Score L/S、Risk、Position、Winrate、Profit Factor