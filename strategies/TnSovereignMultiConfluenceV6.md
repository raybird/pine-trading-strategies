# TnSovereignMultiConfluenceV6 — TeleNexus ICT 多重匯聚主權框架

**版本**: v26.0604.1830 | **移植自**: QuantAlgo smc-pro-multi-confluence-strategy

## 核心邏輯
ICT 三層篩選：HTF 偏向確認 → 流動性獵取偵測 → 訂單塊/FVG 入場。使用 UDT (ZoneData/LiqData) 管理繪圖物件，記憶體受限防洩漏。

## 主要功能
- **HTF 偏向**: 自訂時框（預設 240），反重繪處理
- **流動性獵取**: 擺動高/低等價線偵測 BSL/SSL 掃除
- **訂單塊引擎**: 位移確認 + 顏色編碼 + 減輕（mitigate）標記
- **FVG 引擎**: 最小尺寸過濾 + 自動減輕
- **CRT 確認**: 位移倍數過濾
- **三模式 SL**: Zone / Swing / Sweep 自適應
- **時段過濾**: 倫敦/紐約可選，PDH/PDL 參考線

## 參數
- HTF Timeframe: 240
- Swing Sensitivity: 5
- Min FVG Size: 3 pips
- Displacement Mult: 1.5x ATR
- Risk %: 1.0%, Target RR: 4.0
- SL Type: Zone / Swing / Sweep

## Dashboard
HTF Bias、Trend、Liquidity、Session、Win Rate、Profit Factor、Total Trades、Max DD%