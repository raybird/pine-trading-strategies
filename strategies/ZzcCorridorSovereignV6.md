# Zzc Corridor Sovereign v6

## 策略概述
這是一款基於 **ZigZag Corridors (ZZC)** 框架深度重構的主權策略，採用 Pine Script v6.0 標準構建。它不僅利用非重繪的波段結構進行市場定位，更整合了 **Keltner Channels**、**Donchian Channels** 以及 **BB/KC Squeeze (擠壓)** 偵測技術，旨在捕捉市場從壓縮向擴張轉換時的高動能機會。

## 核心特性
- **主權波動率走廊 (Sovereign Corridor)**:
    - 結合了 Keltner（動態波動率）與 Donchian（物理極值）走廊，定義了精確的執行邊界。
- **因果審計閘門 (Causal Audit Gates)**:
    - **Squeeze 審計**: 監測布林帶 (BB) 是否收縮進肯特納通道 (KC)，識別市場的「儲能」狀態。
    - **Wyckoff SOW 審計**: 識別「弱勢跡象 (Sign of Weakness)」，過濾掉缺乏物理動能支持的虛假突破。
- **高動能突破邏輯**: 僅在擠壓釋放 (Squeeze Release) 且價格突破物理走廊邊界時發出進場指令。
- **實時審計 HUD**: 在圖表右上角披露擠壓狀態、Wyckoff 審計結果與實時波動率，達成執行過程的 100% 透明。

## 模組說明
1. **波段規訓 (ZigZag Settings)**: 負責市場結構的定標。
2. **走廊規訓 (Corridor Envelopes)**: 建立物理執行地板。
3. **因果審計 (Causal Audit)**: 執行 Squeeze 與 Wyckoff 邏輯。
4. **Sovereign HUD**: 提供實時執行狀態審計。

## 使用建議
- **推薦標的**: 指數、商品期貨、高波動率加密貨幣。
- **推薦時框**: 15M (執行) 或 4H (波段)。
- **版本號**: v26.0420.0603
