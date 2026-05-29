# Stochastic Divergence Strategy v6

## 策略名稱與來源
- **名稱**: Stochastic Divergence Strategy v6
- **來源**: [JoelPasapera/Strategies-in-Pine-Script-v6](https://github.com/JoelPasapera/Strategies-in-Pine-Script-v6) — 一個專門收集 Pine Script v6 策略的儲存庫（8 Stars, 最新更新 2026-05-24）
- **原始檔案**: `Stochastic Divergence Strategy/Stochastic Divergence Strategy.pine`

## 核心邏輯摘要
本策略利用價格與 Stochastic 振盪器 %D 線之間的經典背離來進行交易。當價格創更低低點而 %D 創更高低點時，判定為**多頭背離**（buy）；當價格創更高高點而 %D 創更低高點時，判定為**空頭背離**（sell）。使用 5-bar pivot 偵測高低點，並以百分比止損（SL）和止盈（TP）管理風險。多時間框架測試顯示在 EURUSD、USDCHF、AUDUSD 等主要外匯對上從 1 分鐘到 1 小時 K 線均有穩定表現。

## 參數說明

### 風險管理 (Risk Management)
| 參數 | 類型 | 預設值 | 說明 |
|------|------|--------|------|
| Contracts per Trade | int | 1 | 每筆交易合約數量 |
| Use Stop Loss | bool | true | 啟用止損 |
| Stop Loss (%) | float | 2.0 | 止損百分比 |
| Use Take Profit | bool | true | 啟用止盈 |
| Take Profit (%) | float | 4.0 | 止盈百分比 |

### 隨機指標設定 (Stochastic Settings)
| 參數 | 類型 | 預設值 | 說明 |
|------|------|--------|------|
| %K Length | int | 14 | %K 線週期 |
| %K Smoothing | int | 1 | %K 平滑參數 |
| %D Smoothing | int | 3 | %D 平滑參數 |

### 背離設定 (Divergence Settings)
| 參數 | 類型 | 預設值 | 說明 |
|------|------|--------|------|
| Pivot Lookback Left | int | 5 | 樞軸點左側 bar 數 |
| Pivot Lookback Right | int | 5 | 樞軸點右側 bar 數 |
| Max Bars to Look Back | int | 100 | 最大背離掃描範圍 |
| Remove Broken Divergences | bool | true | 自動移除失效背離線 |

## 回測建議
- **推薦市場**: EURUSD, USDCHF, AUDUSD（已驗證）、其他主要外匯對、黃金（XAUUSD）
- **推薦週期**: 1 分鐘 ~ 1 小時（已驗證）；4 小時以上效果遞減
- **風險配置**: 建議帳戶權益的 1-2% 作為每筆風險，SL 2%/TP 4% 為初始設定
- **參數調優**: 可根據不同資產波動率調整 pivot lookback（波動大時增大）、SL/TP 百分比
- **注意**: 震盪盤中背離信號可能頻繁出現導致多次止損，建議搭配趨勢濾波器（如 200 EMA）

## 引用來源
- GitHub Repository: https://github.com/JoelPasapera/Strategies-in-Pine-Script-v6
- 原始策略檔案: `Stochastic Divergence Strategy/Stochastic Divergence Strategy.pine`