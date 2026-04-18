# TN Stacked Imbalance Sovereign v6 (堆疊失衡主權版)

## 策略概述
此策略致力於識別市場中的「強力推動區」。透過對 K 線內部的每一層價格進行掃描，它能精確捕捉到連續出現的買賣失衡（Stacked Imbalance）。這種現象通常代表機構資金正以極高的積極性進行掃單，是市場即將啟動或趨勢延續的高信號指標。

## 核心特性
- **微觀堆疊演算 (Stacked Detection Engine)**: 透過自定義 `method` 對 v6 `footprint` 行對象進行遍歷，即時計算連續的失衡層數，排除單點失衡造成的偽信號。
- **三級感知規訓 (Sensing Modes)**:
  1. **Pulse**: 2 層堆疊，適合高頻或極短線波動捕捉。
  2. **Sovereign**: 3 層堆疊，代表機構級資金的正式介入。
  3. **Conservative**: 4 層堆疊，僅在極強的共識驅動下執行。
- **因果趨勢對焦 (VWAP & SMA)**: 僅在價格位於 VWAP 與 SMA 50 上方（或下方）時才執行失衡進場，確保「微觀失衡」與「宏觀趨勢」的物理同步。
- **因果日誌稽核 (Causal Logging)**: 使用 v6 內建的 `log.info` 實時記錄觸發時的堆疊詳情，為後續的因果分析提供實體證據。

## 模組說明
1. **Footprint Analyzer**: 核心處理模組，負責解析物理行數據。
2. **Imbalance Logic**: 動態判定買賣力量的物理失衡比。
3. **Trend Regulator**: 結合 VWAP 提供動態趨勢邊界。
4. **Execution Dashboard**: 即時披露當前 Delta 增量與規訓模式。

## 使用建議
- **主週期**: 建議在 5M 或 15M 週期下執行，以獲得最佳的微觀細節。
- **失衡門檻**: 建議初始設定 `imbRatio` 為 3.0。
- **版本號**: v26.0418.0715
