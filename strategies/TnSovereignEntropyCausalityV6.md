# TnSovereignEntropyCausalityV6 (v26.0506.0830)

> **「因果不是相關性，而是信息的定向流動。」**

## 1. 核心精髓 (Essence)
本策略是 TeleNexus **Curiosity Engine** 研究成果的實體化資產。它透過 **轉移熵 (Transfer Entropy)** 的簡化算法，量化成交量與價格之間的定向信息傳遞。與傳統技術指標不同，它不關心價格的高低，而關心「誰在驅動誰」。僅當成交量的信息流顯著領先價格位移時，系統才承認該趨勢的主權合法性。

## 2. 三位一體因果鏈 (Causal Chain)
- **符號動力學編碼 (Symbolic Encoding)**: 將原始 K 線數據轉化為離散狀態（上漲、持平、下跌），消除幅度雜訊，專注於事件序列的拓撲結構。
- **定向信息傳遞 (Information Transfer)**: 透過計算 $V_{t-1} \rightarrow P_t$ 的條件機率，識別市場的「領先/滯後」關係。$\Delta TE > 0.1$ 被定標為機構驅動的硬性門檻。
- **分形維度對位 (Fractal Alignment)**: 整合昨日 Kronos V12 的分形效率指標。僅在路徑效率高（低分形維度）的區間執行，過濾掉高熵的隨機震盪。

## 3. 性能指標 (Expected Performance)
- **環境**: 1M / 5M (適用於高頻訂單流交互頻繁的標的)。
- **特徵**: 極高信噪比，能有效識別「無量空拉」或「虛假對敲」後的陷阱。
- **止損**: ATR 動態對位止損，兼顧波動率聚類的生存空間。

## 4. 規訓記錄 (Audit Log)
- **v26.0506.0830**: 首版實體化。將轉移熵算理接入 Pine Script v6，實現了非線性因果的實時視覺化與審計。

---
*Calibrated at Wed May 6 08:30:23 CST 2026 | Calibration: Sovereign*
