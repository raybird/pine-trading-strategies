# TnSovereignSnrQmrRnsV6 — TeleNexus 多時框 SNR / QMR / RNS 共流感合策略

## 概述
移植自 `cuci1995/msnr-qmr-rns-strategy`（無顯式授權）`MSNR_QMR_RNS_Strategy_v2.pine`（v2，2026-09-01 建立，36K 行級 strategy() 自足無外部 lib）。以 **SNR（原始支撐/阻力區間）、Quasimodo（QMR）反轉型態、RNS（角色翻轉再生）** 三層結構引擎，於 W/D/H4/H1 四時框各自建構「新鮮未觸」結構區，並以 **MSNR 共流感合計數** 把關：同一新鮮區與其他時框新鮮區重疊數 ≥ `minConfluence`（預設 3，含觸發時框）才允許進場。輔以 W/D Open-Close 偏見過濾、RNS 觸發之吞噬/針棒 K 線確認、與 LTF（H1/M30/M15）結構縮停的 R:R（預設 1:5）風控。精髓在於「時框共感的結構位階」取捨，而非單一時框追逐突破。

## 核心邏輯
- **SNR 區間建構**：每時框以 `ta.pivothigh/low(pivotLen)` 已確認樞軸為外緣（影線極值 ± buffer），開/收實體邊界為內緣，構成支撐/阻力帶；`maxZonesPerTF` 限量淘汰最舊
- **QMR（波那）型態**：三樞軸歷史 `Low→High→Low2(破 Low1)` → 收盤站回 High1 確認 BUY 區（在 Low1），賣方對稱 `High→Low→High2(破 High1)` → 收盤破 Low1 確認 SELL 區；僅收盤穿越觸發線後成立（非重繪）
- **RNS 翻轉**：任一區間被「實體收線穿越其外緣」mitigate → 原角色刪除並於原帶再生為 `RNS` 翻轉區（舊支撐 → 新阻力），需吞噬/針棒確認（`useCandleConfirmRNS`）
- **MSNR 共感計數**：`f_countConfluence` 逐時框比對新鮮·未破·重疊區（`f_overlap`），每一時框 +1；達 `minConfluence` 門檻才觸發
- **偏見濾網**：`useOpenCloseBias` 要求收盤 > D/W Open 才允買（賣方對稱），可關閉
- **曝險紀律**：`oneTradeAtATime`（持倉時忽略新訊號）、`useDateRange` 回測窗、單日單 bar 一筆

## 風險管理
- **R:R bracket**：停損出於區間外緣或 LTF 結構縮停（`f_refineSLBuy/Sell` 取最緊且有效之 H1/M30/M15 擺動）＋ SL buffer（tick）
- 目標 `rrTarget`（預設 1:5）為停損幅度之倍數；倉位依 `strategy.equity × riskPct% / 風險` 計算
- `pyramiding=0`、單一持倉；`strategy.exit` stop/limit 雙向 bracket

## Sovereign Overlays
- 四時框（W/D/H4/H1）SNR 區間 + 樞軸型態歷史（type/value/oc-edge 各 6 筆）
- Quasimodo 三樞軸型態偵測（收線確認、非重繪）；RNS 角色翻轉引擎
- MSNR 共流感合計數 + Min TF 門檻；W/D Open-Close 偏見濾網
- RNS 吞噬/針棒 K 線確認；LTF 結構縮停 + 1:5 R:R + 權益% 倉位
- JSON Webhook `alert()`（含版號欄位）+ `alertcondition` 靜態告警
- 統計表：成交/勝/敗/勝率/獲利因子/淨利 + 版號鎖定
- `ta.lookahead_off` 取價（非重繪契約）；輸入群組化防呆預設

## 版號
- 版本：v26.0909.1830
- 審計時間：2026-09-09 18:30 CST
- 來源：cuci1995/msnr-qmr-rns-strategy（無顯式授權；邏輯為策略之工程化近似，僅供研究，實盤前請自行驗證）