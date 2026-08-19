# TnSovereignIctLsReversalV6 — TeleNexus 主權 ICT 流動性掃蕩反轉策略

## 概述
移植自 `pranay123-stack/Tradingview_Pinescript_Strategy` 的 `crypto_ict_liquidity_sweep_reversal_v1.pine`（2026-08-20 初始發布，研究級非重繪，~1565 行）。將 ICT/SMC 的流動性掃蕩反轉鏈轉化為確定性、可回溯的 v6 策略，核心狀態機以 10 態嚴格執行因果鏈：

```
HTF BIAS → LIQUIDITY → SWEEP → DISPLACEMENT → MSS/CHoCH → FVG → FVG 回撤入場 → 對向流動性 TP
```

## 10 態狀態機
IDLE → WAIT_SWEEP → SWEEP → DISP → MSS → FVG → WAIT_RETR → ENTRY → IN_POS（INVALID 為瞬態，同一根收盤重置回 IDLE）。

## 非重繪契約
- `calc_on_every_tick = false`：所有決策僅在收盤價（closed bar）執行，歷史與即時邏輯同位。
- `request.security` 統一使用 `barmerge.lookahead_off`，且以 HTF 收盤時間閘門確認後才採納（HTF bar 結束才更新偏見）。
- `ta.pivothigh/pivotlow` 僅在確認棒（n 根後）消費，pivot bar 不會被視為已知。
- 前日/前週高低由已收盤的 chart bar 累積，無 HTF security 合併歧義。

## 流動性註冊表（BSL/SSL 雙池）
- SWING（chart TF 擺動高低）、EQ（等值高低，ATR 容差）、PD（前日）、PW（前週）四來源。
- FIFO prune 至 max levels/side；生命週期規則：收盤穿越即失效；可設定 max age 失效。
- 掃蕩 = 穿越 + 收盤回穿（非觸及、非突破），品質過濾：`maxSweepDist`（×ATR 穿越深度）、`minWickRatio`（蠟燭上/下影拒絕）。

## 位移 / MSS / FVG
- 位移：range > ATR×1.20 且 body/range ≥ 0.60（方向收斂）。
- MSS：位移後需 CHoCH/BOS 結構確認（可關閉）。
- FVG：三燭失衡，min size ≥ ATR×0.05；回撤請單在 FVG 中點/近緣/遠緣；20 根未成交失效。

## 進場與風控
- 入場前閘門：HTF 偏見對齊、session 過濾（London/NY）、日期窗。
- 止損三模：掃蕩無效化 / FVG 無效化 / ATR。
- 目標：對向流動性 / 固定 RR / 混合（部分平倉）；可選 break-even。
- 風險：Risk % of equity 或固定數量、每日交易上限、連敗冷卻、每日虧損上限。

## 移植來源
- 原始倉庫：`pranay123-stack/Tradingview_Pinescript_Strategy`
- 原始檔案：`crypto/Crypto ICT Liquidity Sweep Reversal Strategy v1/strategy/crypto_ict_liquidity_sweep_reversal_v1.pine`
- 發布日期：2026-08-20（4 小時前更新）
- 主權化版本：v26.0820.0630