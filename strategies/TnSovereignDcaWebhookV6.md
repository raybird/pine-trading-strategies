# TnSovereignDcaWebhookV6 (DCA Webhook Execution Engine)

## 策略概述
獵取自 **ggamer5555/Pinescript-v6-strategy-with-Json-Webhook-output-example** 的 DCA 網格引擎核心，以 TeleNexus Sovereign 規範重寫。此策略實作雙重 DCA（均價成本）交易引擎，搭配 BBW 波動率過濾與 JSON Webhook 輸出，可直接橋接至 MT5 外部執行系統。

## 核心特性
- **Sovereign Enum 狀態機**: 使用 `enum DcaState`（IDLE→SETUP→ACTIVE→CLOSING）管理 DCA 生命週期，杜絕布林混亂。
- **雙重 DCA 引擎**:
  1. **Normal DCA**: 標準失衡進場，支援多達 4 層安全訂單（Safety Orders），每層等比放大倉位。
  2. **BBW DCA**: 低波動率（Bollinger Band Width < 閾值）失衡進場，專用於盤整區間的均值回歸獵取。
- **4 層 Sovereign 因果審計**:
  1. EMA 趨勢對位（9/50）
  2. HTF 波動率體質（BBW 240）
  3. 失衡確認（價格突破極值 + 範圍百分比）
  4. 因果評分閾值（≥3 觸發 Sovereign Filter）
- **JSON Webhook 輸出**: 加密密碼驗證的狀態 payload `{side1, side2, TP1, SL1, trend}`，相容現有 MT5 橋接架構。
- **ATR 移動停損**: 動態追蹤止損，避免固態百分比被過度波動掃出。

## 模組說明
1. **Volatility Regime Module**: BBW 高時框波動率分類（LOW/NORMAL/HIGH），決定啟用哪套 DCA 引擎。
2. **DCA State Machine**: 追蹤正常/BBW 兩套 DCA 的狀態機，管理進場→安全訂單→出場的生命週期。
3. **Sovereign Causal Audit**: 4 層評分系統（0-4），確保僅在因果條件充分時觸發。
4. **Webhook Serializer**: 將當前交易狀態序列化為 JSON，透過 `alert()` 推送給外部執行系統。

## 使用建議
- **主週期**: 15M 或 1H（適合 DCA 網格策略的特性）。
- **BBW 高時框**: 240（4H），用於判定波動率體質。
- **建議對應**: BTCUSD / ETHUSD 等高波動率加密貨幣（DCA 在趨勢中平均成本效果顯著）。
- **版本號**: v26.0527.0630
- **靈感來源**: ggamer5555 LIVE ALERTS PYTH MT5 Strategy

## Webhook Payload 格式
```json
{
  "passphrase": "telenexus_sovereign",
  "side1": "1",
  "side2": "0",
  "TP1": "68500.25",
  "SL1": "66100.00",
  "trend": "1"
}
```
- `side1`: Normal DCA 方向（1=多, -1=空, 0=持平）
- `side2`: BBW DCA 方向（同上）
- `trend`: EMA 趨勢（1=多頭, -1=空頭, 0=中性）