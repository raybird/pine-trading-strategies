# TnSovereignIctSniperV6 — TeleNexus 主權 Prop Firm ICT 狙擊策略（生存模式）

## 概述
移植自 `thesenegalesehitch/Pine-Script` 的 `ict-sniper.pine`（Prop Firm ICT Sniper | Survival Mode，作者 Alexandre Albert Ndour）。以 ICT 狙擊概念（買/賣方流動性掃蕩 + 位移 FVG）為核心，搭配 PropFirm 生存模式風控體系，確保每一筆交易都嚴格遵守「風險先行」紀律。

## 核心邏輯

### 市場結構與流動性（Sweep）
- 以 `ta.pivothigh/low` 偵測擺動高/低點
- **BSL（Buy-Side Liquidity）掃蕩**：價格突破前高後收回，觸發賣方狙擊前提
- **SSL（Sell-Side Liquidity）掃蕩**：價格跌破前低後收回，觸發買方狙擊前提

### Displacement 與 FVG
- 位移確認：實體 K 線大於 `ATR × 1.5`，排除無效盤整
- **多頭 FVG**：`low < high[2]` 失衡區，需大於最小 Pips 門檻
- **空頭 FVG**：`high > low[2]` 失衡區，需大於最小 Pips 門檻

### 狙擊入場（A+ 條件）
- **BUY**：SSL 掃蕩 + 多頭 FVG，價格位於 FVG 下緣至頂部區間
- **SELL**：BSL 掃蕩 + 空頭 FVG，價格位於 FVG 底部至頂部區間

## 生存模式風控
- **Phase 風險縮放**：Phase 1 / Phase 2 各自獨立風險 %（如 1.0% / 0.5%）
- **每日虧損硬限制**：以初始資本計算上限，觸及即停止開新倉
- **每日 P&L 重置**：換日自動歸零累計
- **權益風險倉位**：`倉位 = 風險金額 / 停損距離`，每筆風險固定比例權益

## 風險管理
- 動態 SL/TP：以 FVG 邊界 + `mintick × 5` 計算停損距離，TP 為 SL × R:R
- 單筆倉位完全由風險金額與停損距離反推

## 移植來源
- 原始倉庫：`thesenegalesehitch/Pine-Script`
- 原始檔案：`pine-scripts/strategies/ict-sniper.pine`
- 主權化版本：v26.0802.1830
