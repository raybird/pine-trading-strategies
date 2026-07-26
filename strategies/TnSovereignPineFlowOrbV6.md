# TnSovereignPineFlowOrbV6 — TeleNexus 主權 PineFlow ORB 策略

## 概述
移植自 `loveyuanfandj-glitch/pineflow-v6` 的 `pineflow_orb_strategy.pine`（2026-07-24 發布）。Opening Range Breakout（開盤區間突破）策略，加入 HTF EMA 趨勢確認、DMI/ADX 趨勢強度過濾與權益風險 ATR 倉位計算。

## 核心邏輯
1. **開盤區間累積**：可配置時段（預設 NY 0930-1000），期間追蹤區間高/低點
2. **趨勢確認**：Fast/Slow EMA 對位 + HTF EMA 非重畫確認 + DMI/ADX 趨勢強度門檻
3. **突破入場**：收盤價突破區間高/低點時觸發，方向與趨勢過濾一致
4. **倉位計算**：基於帳戶權益風險百分比 + ATR 停損距離的動態口數
5. **兩層獲利**：50% 倉位於 1.5R 部分出場，50% 於 3.0R 出場
6. **風險限制**：最大日虧損、最大回撤、每日交易次數上限

## 過濾器
- Fast/Slow EMA 趨勢濾網
- HTF EMA 趨勢確認（lookahead_on 非重畫）
- DMI/ADX 趨勢強度（預設 ADX ≥ 20）
- 交易時段閘門
- 每日交易次數限制

## 風險管理
- 權益風險百分比倉位計算
- ATR 動態停損
- 兩階段獲利了結（50%@1.5R, 50%@3.0R）
- 最大日虧損限制
- 最大回撤限制
- 交易時段結束強制平倉

## 移植來源
- 原始倉庫：`loveyuanfandj-glitch/pineflow-v6`
- 原始檔案：`pine/pineflow_orb_strategy.pine`
- 發布日期：2026-07-24
- 主權化版本：v26.0727.0630
