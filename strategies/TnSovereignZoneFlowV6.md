# TnSovereignZoneFlowV6 — TeleNexus 樞軸區間 Break-and-Retest 紐約盤尖形策略

## 概述
移植自 `anirudh-annamaneni/tradingview-indicators`（MIT）`strategies/spx-zoneflow-validation/SPX_ZoneFlow_Validation.pine`（v2.0，2026-09-01 更新）。以 **樞軸區間 (Pivot-Zone)** 為結構核心的紐約盤交易引擎：在 Zone TF（預設 5m）以已確認樞軸高/低點透過最小動能 `minImpulseAtr` 建構多空腿區間，並依腿長投影 **POI / OTE 0.618-0.705 / Mitigation 0.705-0.786 / 1.272 目標**。Bias TF（預設 30m）提供結構偏見，微樞軸突破建立 Break 旗標後，僅接受「區間內回踩重測（Break-and-Retest）+ 拒絕K線品質」的確認觸發。整條決策鏈再以地點品質評分（Location Score）與三維 Regime Score（ADX/ATR/斜率/方向效率）把關，取的是「突破後的結構性延續」而非追逐突破本身。

## 核心邏輯
- **樞軸區間建構**：Zone TF 樞軸 + `minImpulseAtr` 動能濾網 → 自動整併（merge）多空腿區間，投影四象限關鍵價位
- **偏見引擎**：Bias TF（30m）結構偏見 + 偏見幅度評分（25 + 45·ADXnorm + 30·momentum）
- **觸發紀律**：微樞軸 Break 旗標（3 bar 回踩窗 + 容差）→ Break-and-Retest 確認，需拒絕K線品質（wicks/body/量能）
- **Regime Score 0-100**：ADX·0.35 + ATR·0.20 + 斜率·0.25 + 方向效率·0.20，具進出遲滯避免頻繁切換
- **Location Score**：寬度·0.35 + 新鮮度·0.30 + R:R·0.35，過濾稀薄/過舊/低值區域
- **NY 時段引擎**：09:30-16:00 RTH 入場窗、11:30-13:30 午餐模式（硬封/降信心/體制+量能）、開盤暖機、跳空隔離

## 風險管理
- 自適應結構停損（區間失效）＋ ATR 停損；相對轉向動能失效即離場
- **PT1 / PT2 兩段部分平倉** + 15:55 收盤前強制平倉
- Lunch Shadow 診斷模式（只出訊號不下單）；單一倉位、權益百分比倉位（`qty_percent`）
- 多/空獨立開關；跳空日與資料新鮮度隔離

## Sovereign Overlays
- Pivot-Zone 建構（POI / Optimal / Mitigation / Target 1.272｜merge 自動整併）
- HTF 結構偏見（Bias）+ 偏見幅度評分；Session EMA（開盤錨定）+ 歷史 EMA 備援
- Regime Score 0-100 進出遲滯；Webhook 就緒 `alertcondition`
- HUD 表：區間與狙擊帶、Location/Regime 分數、優先方向、持倉與目標、版號
- `ta.lookahead` 確認樞軸（`barmerge.lookahead_on`）+ `runtime.error` 輸入防呆

## 版號
- 版本：v26.0909.0630
- 審計時間：2026-09-09 06:30 CST
- 來源：anirudh-annamaneni/tradingview-indicators（MIT）