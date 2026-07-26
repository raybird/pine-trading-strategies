# TnSovereignPineFlowIctFvgV6 — TeleNexus 主權 PineFlow ICT FVG 執行模型

## 概述
移植自 `loveyuanfandj-glitch/pineflow-v6` 的 `pineflow_ict_fvg_strategy.pine`（2026-07-24 發布）。三層確定性 ICT 執行模型，操作於 4H → 15m → 1m 時框堆疊，每一層需獨立確認後信號才觸發。

## 三層架構

### Layer 1 — 4H 情境 (Context)
- EMA 50 偏見過濾（多/空傾向）
- 擴張/回調相位分類
- 4H FVG 偵測（多頭/空頭失衡區）

### Layer 2 — 15m 設置 (Setup)
- 確認 4H FVG 觸及
- 賣方/買方流動性掃蕩偵測
- FVG 形成 + MSS（市場結構轉變）/ CISD（交付狀態改變）確認
- 設置候選有過期時間（預設 240 分鐘）

### Layer 3 — 1m 觸發 (Trigger)
- 回撤至設定 FVG 區域
- 1m 樞軸流動性掃蕩
- 1m FVG 形成 + MSS/CISD 突破
- 觸發候選有過期時間（預設 90 分鐘）

## 入場邏輯
- **多方**：4H 多頭偏見 → 4H FVG 觸及 + 15m 賣方掃蕩 → 15m FVG + MSS/CISD → 1m 回撤至 FVG → 1m 掃蕩 + FVG + MSS/CISD
- **空方**：4H 空頭偏見 → 4H FVG 觸及 + 15m 買方掃蕩 → 15m FVG + MSS/CISD → 1m 回撤至 FVG → 1m 掃蕩 + FVG + MSS/CISD

## 風險管理
- 權益風險百分比倉位計算
- 流動性掃蕩極值停損（或 ATR 備援停損）
- 擺動高/低點獲利目標（或 ATR 備援目標）
- 最大日虧損與最大回撤限制
- 每日交易次數限制

## 移植來源
- 原始倉庫：`loveyuanfandj-glitch/pineflow-v6`
- 原始檔案：`pine/pineflow_ict_fvg_strategy.pine`
- 發布日期：2026-07-24
- 主權化版本：v26.0727.0630
