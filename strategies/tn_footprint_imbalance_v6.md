# TN Footprint Imbalance Sovereign v6 (訂單流失衡主權版)

## 策略概述
此策略代表了 TeleNexus 對「微觀交易主權」的深度實踐。它透過 Pine Script v6 的原生 `request.footprint()` 函數，直接審計價格內部的買賣成交分佈，捕捉控制點 (POC) 處發生的物理失衡。相較於傳統指標，此策略能更直接地感知市場共識的「力竭」與「爆發」。

## 核心特性
- **原生 Footprint 對位**: 全量使用 v6 `footprint` 與 `volume_row` 內建物件，精確提取 POC 價格、買入量與賣出量。
- **三級主權規訓 (Risk Profiles)**:
  1. **Aggressive**: 300% 失衡門檻，捕捉早期動能。
  2. **Balanced**: 400% 失衡門檻，兼顧信號品質與頻率。
  3. **Sovereign**: 500% 失衡門檻，僅在極端因果對位下執行。
- **因果雙重驗證**: 不僅要求 POC 發生失衡，還要求整根 K 線的累積 Delta 與失衡方向一致，確保執行路徑具備高度的一致性。
- **動態 ATR 防禦**: 基於市場波動率實時計算止損空間，確保執行主權不被市場雜訊侵害。

## 模組說明
1. **Footprint 獲取層**: 執行 `request.footprint` 並定義價格聚合區間 (Ticks)。
2. **失衡審計引擎**: 透過 `switch` 語句根據規訓等級動態判定 `isBullishImbalance` / `isBearishImbalance`。
3. **執行模組**: 結合 POC 數據與 Delta 定向觸發 `strategy.entry`。
4. **實時指標看板**: 利用 `str.format` 在圖表端點即時披露當前的失衡數據。

## 使用建議
- **主週期**: 5M 或 15M (訂單流分析的最佳窗口)。
- **Tick 聚合**: 根據標的波動性調整 `ticksPerRow`。
- **版本號**: v26.0418.0715
