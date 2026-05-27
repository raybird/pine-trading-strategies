# TeleNexus Fakeout Signal Quality v6 — trugurpala Port

> **獵取來源**: [trugurpala/pinescriptv6](https://github.com/trugurpala/pinescriptv6) — 18_fakeout_filter (indicator) + 13_fakeout_confirmed_strategy
> **原作**: Ugur Pala
> **移植**: TeleNexus Sovereign Studio | 版號 v26.0528.0630
> **授權**: MIT (保留原作者署名)

---

## 核心邏輯

此指標／策略實作 **4 層信號品質過濾器**，用於判斷價格行為是否為可信賴的交易信號，或僅為市場雜訊／假突破：

1. **Layer 1 — Volume Confirmation**：成交量 > 20 SMA × 1.5（可調），排除低量假信號
2. **Layer 2 — HTF Trend Filter**：高時框（H1/H4/D1）EMA 趨勢方向對位，避免逆勢交易
3. **Layer 3 — ATR Volatility Band**：價格觸及 ±2 ATR 邊界時才視為有效信號，提升突破門檻
4. **Layer 4 — Bar Structure**：Outside Bar 過濾（高 > 前高 且 低 < 前低），確認價格意圖

---

## 信號品質評分

| 分數 | 標籤 | 顏色 | 建議動作 |
|------|------|------|----------|
| 0 | Very Low | 🔴 | 忽略，高度不可信 |
| 1 | Low | 🟠 | 僅作為觀察 |
| 2 | Medium | 🟡 | 僅結合其他確認 |
| 3 | High | 🟢 | 可考慮進場 |
| 4 | Very High | 🟢🟢 | 高可信度，建議執行 |

---

## TeleNexus 主權擴展

相較於原版，此移植版本添加以下主權特徵：

- **視覺化品質分數圖表**：即時顯示 0-4 品質曲線
- **Last Bar 診斷面板**：在圖表末根 K 棒顯示每層狀態
- **可參數化閾值**：所有過濾層的參數皆可於設定面板調整
- **策略就緒**：可輕鬆嵌入 strategy() 作為進場條件

---

## 用法

```pine
// 在你的策略中引用信號品質：
if signalQuality >= 3
    strategy.entry("Long", strategy.long)
```

---

## 檔案

| 檔案 | 說明 |
|------|------|
| `tn_fakeout_signal_quality_v6.pine` | Pine Script v6 實作 |
| `tn_fakeout_signal_quality_v6.md` | 策略說明文件 |

---

*Ported with gratitude to trugurpala for the original 4-Layer Fakeout Filter concept.*