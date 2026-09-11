# TnSovereignRsiStateDivConfluenceV6

> **TeleNexus Sovereign Trading Systems — Pine Script v6**
> Version: `v26.0911.1830` · Causal Audit: `2026-09-11 18:40 CST`

## 策略定位

**RSI-50 狀態機 + 隱藏背離 + 三重可切換匯流濾網**的主權移植。

交易者從 RSI 中性線（預設 50）的「穿越 → 遠離 → 重測」三拍節奏中計時，只承接
**隱藏背離 (hidden divergence)** 確認之延續，並以 EMA touch、Fibonacci 黃金回撤帶
與 Ichimoku Kumo 三枚可切換匯流濾網提高 set-up 成熟度。停損鎖定最後擺盪點，
獲利以可配置 R:R 倍率 bracket 出場。

## 與現有庫之差異

現有背離系策略（`StochDivergenceV6` / `CMOV6` / `OscDivZonesV6`）為**單一振盪器**
的裸背離或統計外緣穿越，缺少「RSI 中性線時序狀態機」計時紀律。本策略保留完整
四態機（穿越 → 遠離 → 重測 → 隱藏背離確認），輔以三重匯流濾網，填補
**「RSI 中性線 pullback 時序」+「hidden divergence 延續」+「多濾網共感」**
紀律缺口。

## 核心邏輯

### 1. RSI 中性線狀態機（State 0→1→2→3）
- **State 0** — 等待 RSI 穿越中性線（穿越向上 → long bias，向下 → short bias）。
- **State 1** — RSI 必須偏離觸發線至少 `RSI retest buffer`（預設 5.0），再回測觸發區。
- **State 2→3** — 隱藏背離確認 set-up：
  - 多頭：價位 higher low + RSI lower low
  - 空頭：價位 lower high + RSI higher high
- **失效機制** — set-up 超過 `Setup expiry`（預設 30 bars）自動歸零；反向穿越亦重置。

### 2. 隱藏背離偵測
以 `ta.pivotlow / ta.pivothigh`（左 5 / 右 5）捕捉已確認樞軸，建構前後二次樞軸比較，
pivot 於右側確認後才成立（無重繪）。

### 3. 三重可切換匯流濾網（個別可獨立開關）
| 濾網 | 條件 |
|------|------|
| **EMA touch** | 價格實體觸及 20 EMA（低航 ≤ EMA ≤ 高） |
| **Fibonacci zone** | 價格回撤至最後擺盪腿的 0.5–0.618 帶內 |
| **Ichimoku cloud** | 觸雲模式（ON）或長/短方向雲側位置（OFF） |

### 4. 風險管理
- **停損** — 最後擺盪低點（多）/ 高點（空）。
- **目標** — `停損距離 × Reward:Risk`（預設 2R）。
- **倉位** — `percent_of_equity` 10%、`pyramiding = 0` 單一持倉。
- **JSON Webhook** — Long/Short 進場附 entry/stop/tp 現價送出。

## 參數表

| 群組 | 參數 | 說明 | 預設 |
|------|------|------|------|
| Filters | Use EMA / Fib / Ichimoku | 三濾網獨立開關 | true |
| EMA | EMA Length | 趨勢 EMA 長度 | 20 |
| RSI | RSI Length | RSI 週期 | 14 |
| RSI | RSI Trigger Level | 中性觸發線 | 50.0 |
| RSI | RSI retest buffer | 有效重測前所需偏離距離 | 5.0 |
| RSI | Setup expiry | 未完成 set-up 失效條數 | 30 |
| Pivot | Pivot left / right bars | 樞軸偵測窗 | 5 / 5 |
| Fibonacci | Fib level 1 / 2 | 回撤帶邊界 | 0.5 / 0.618 |
| — | Reward : Risk | 目標倍率 | 2.0 |
| — | Trade Long / Trade Short | 方向開關 | true |
| Ichimoku | Conversion / Base / SpanB / Lagging | 雲參數 | 9/26/52/26 |
| Ichimoku | Cloud Touch Mode | 觸雲或雲側模式 | true |

## 異動記錄

- **v26.0911.1830** — 獵頭審計 #139：GitHub 全數檢索新出現 `moonyroy/trust-me-bro-strategy`
  （MIT，2026-09-06 初始發佈）。RSI 中性線三拍狀態機 + 隱藏背離 + 三重匯流確認，
  現有庫之 StochDivergence/CMO/OscDivZones 均為單一振盪器裸背離，補此紀律缺口。
  移植為 `TnSovereignRsiStateDivConfluenceV6`，歸 **Mean Reversion & Oscillator 23→24**。

## 聲明

*執行主權，因果必達。本策略由 MIT 授權來源重寫，非金融投資建議，請自行回測驗證。*