# TnSovereign Supertrend Volume V6

## 策略版本
- **版本**：v260517.1830
- **更新時間**：2026-05-17 18:30 CST

## 策略說明

結合 Supertrend 趨勢判斷與 Volume 過濾的混合策略。Supertrend 採用 ATR 作為波動標準，結合成交量放大確認信号強度，減少假突破。

## 核心邏輯

1. **Supertrend 計算**
   - 使用 ATR（Length=10）計算上下軌
   - Multiplier=3.0 控制敏感度
   - 趨勢方向根據收盤價與前一波超級趨勢關係判定

2. **Volume 確認機制**
   - 成交量高於 20 期均線的 1.5 倍視為確認信號
   - 可開關是否強制要求成交量確認

3. **交易信號**
   - 多頭：Supertrend 上升 +（可選）成交量放大
   - 空頭：Supertrend 下降 +（可選）成交量放大

## 參數說明

| 參數 | 預設值 | 說明 |
|------|--------|------|
| ATR Length | 10 | ATR 計算週期 |
| Supertrend Multiplier | 3.0 | ATR 倍數，越大越遲緩 |
| Volume MA Length | 20 | 成交量均線週期 |
| Volume Threshold | 1.5 | 成交量放大倍數 |
| Require Volume Confirm | true | 是否强制成交量確認 |

## 適用市場

- 流動性較高的個股、期貨
- 盤整突破後的顺势行情
- 不適合低成交量市場

## 風險提示

- Multiplier 過高會延遲信號
- 成交量確認可能过滤部分有效信号
- 需結合其他指標確認趨勢強度
