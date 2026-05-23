# Tn Sovereign Katana Flow v6

| 元數據 | 值 |
|--------|-----|
| **版本** | v26.0523.1830 |
| **類型** | Strategy |
| **Pine Script** | v6 |
| **實體化時間** | 2026-05-23 18:30 CST |

## 核心邏輯

Twin Range Filter（雙平滑範圍濾波器）— 透過兩層 SMA 平滑價格區間，再以雙 EMA 二次平滑產出 TRF 數列，搭配動態標準差通道過濾假突破。

### 進場條件
- **多單**: TRF 上穿訊號線、趨勢轉 Bullish、波動率正常
- **空單**: TRF 下穿訊號線、趨勢轉 Bearish、波動率正常

### 出場條件
- ATR 動態停損：$1.5 \times ATR$
- 固定盈虧比停利：$2:1$

### 風險過濾
- ATR 百分位波動率過濾（20%-80% 正常區間外不進場）

## 參考來源
- KatanaFlow Twin Range Filter, 7mertyavuz (GitHub)
- 經 TeleNexus Sovereign 主權化重寫