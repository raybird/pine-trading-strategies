# TN Compression Expansion v6 (ATR 壓縮突破版)

## 策略概述
基於波動率壓縮後的爆發性突破交易。當 ATR 比值低於閥值時辨識為壓縮區，等待價格突破近期區間後進場。不同於 Bollinger/Keltner 通道擠壓，本策略使用純 ATR 比值偵測，計算成本更低且重繪風險更小。

## 核心邏輯
1. **ATR 比值計算**: `atrVal / ta.sma(atrVal, lookback)`，值越低表示波動越壓縮。
2. **壓縮區辨識**: 比值低於 `compressionPct` (預設 0.7) 時標記為壓縮狀態。
3. **區間突破**: 取 `rangeBars` 根 K 線的最高/最低作為區間，收盤價突破時觸發。
4. **評分引擎**: 壓縮中 (+1), 近期壓縮過 (+1), 突破 (+1), 總分 ≥2 才進場。

## 進出場規則
- **進場**: 壓縮狀態 + 區間突破，做多/做空。
- **停損**: 進場價 -/+ `ATR × atrStopMult` (預設 1.5 倍 ATR)。
- **止盈**: 停損距離 × `rrTarget` (預設 2:1 RR)。

## 參數說明
| 參數 | 預設值 | 說明 |
|------|--------|------|
| ATR Length | 14 | ATR 計算週期 |
| ATR SMA Lookback | 20 | ATR 均線參考期數 |
| Compression Threshold | 0.7 | 比值低於此值視為壓縮 |
| Range Lookback | 10 | 近期區間參考 K 線數 |
| ATR Stop Multiplier | 1.5 | 停損的 ATR 倍數 |
| Risk/Reward Ratio | 2.0 | 止盈/停損比 |

## 使用建議
- **主週期**: 15M 或 1H。
- **適用**: 震盪收斂後的趨勢盤。
- **版本號**: v260518.0630