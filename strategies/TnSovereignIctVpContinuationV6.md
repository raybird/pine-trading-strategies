# TnSovereignIctVpContinuationV6 — TeleNexus 主權 ICT 量價輪廓延續策略

## 概述
移植自 `pranay123-stack/Tradingview_Pinescript_Strategy` 的 `ICT_Volume_Profile_Continuation_v1.pine`（2026-08-20 初始發布，MPL-2.0，~1879 行，研究級非重繪）。此為該倉庫「Portfolio Strategy 2 of 2」，採用量價輪廓（Volume Profile）情境的**延續**模型（非掃蕩反轉）：

```
HTF BIAS → VOLUME PROFILE CONTEXT → VALUE ACCEPTANCE → BOS → DISPLACEMENT
        → FVG → RETRACEMENT → CONTINUATION ENTRY → VP/流動性目標
```

## 確定性 Volume Profile（非 TradingView 原生）
- 自製固定 price-bin 直方圖替代（文件明示為確定的近似，非原生 closed-source VP）。
- 可設 rows（價格分箱數）、Value Area %（預設 70）、樣本上限、時區。
- 輸出 POC / VAH / VAL，以及 HVN（高交易量節點 ≥ mean×1.35）與 LVN（低交易量節點 ≤ mean×0.65）。
- 僅由已收盤 bar 累積——profile 於每個期間邊界重建一次，確定且不重繪。

## 價值接受（Acceptance）
- 參考 profile 可選 Previous-Day / Previous-Week。
- 接受條件：N 根連續收盤穿越 VAH（多）或 VAL（空）＋ 可選維持式接受（gap-and-go 連續日）。
- 接受後等待第一個同向 BOS，接續位移 → FVG 回撤延續入場。

## 狀態機
IDLE → BIAS → VALUE → BOS → DISP → FVG → WAIT_RETR → ENTRY → IN_POS（INVALID 瞬態）。

## 延續入場與風控
- FVG 中點/近緣掛單進場，max retracement bars 過期。
- 停損：ATR bracket 或結構（前擺動±buffer）。
- 目標：TP1 部分平倉（%可調）＋ runner 更高 RR；ATR bracket 全程護航。
- 風控：Risk % of equity 或 ATR-scaled、每日虧損上限、每日交易上限。
- 無掃蕩／stop-hunt／反轉邏輯——純 BOS + 位移延續模型。

## 移植來源
- 原始倉庫：`pranay123-stack/Tradingview_Pinescript_Strategy`
- 原始檔案：`crypto/ICT Volume Profile Continuation Strategy v1/ICT_Volume_Profile_Continuation_v1.pine`
- 授權：MPL-2.0
- 發布日期：2026-08-20
- 主權化版本：v26.0820.0630