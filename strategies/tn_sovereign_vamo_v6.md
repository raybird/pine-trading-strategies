# Tn Sovereign VAMO v6

| 元數據 | 值 |
|--------|-----|
| **版本** | v26.0523.1830 |
| **類型** | Strategy |
| **Pine Script** | v6 |
| **實體化時間** | 2026-05-23 18:30 CST |

## 核心邏輯

波動調整動量振盪器（Volatility-Adjusted Momentum Oscillator），將 ROC（動量）以 ATR（波動）標準化，產出無單位的 VAMO 數列，再以 EMA 生成訊號線。

### 進場條件
- **多單**: VAMO 上穿訊號線、VAMO > 0、波動率在正常區間
- **空單**: VAMO 下穿訊號線、VAMO < 0、波動率在正常區間

### 出場條件
- ATR 動態停損：$1.5 \times ATR$
- 固定盈虧比停利：$2:1$

### 風險過濾
- 波動率百分位篩選：僅在 ATR 低於第 80 百分位時交易

## 參考來源
- VAMO Strategy, TPTBusiness (GitHub)
- 經 TeleNexus Sovereign 主權化重寫