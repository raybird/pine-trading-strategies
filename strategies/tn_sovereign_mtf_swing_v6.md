# Tn Sovereign MTF Swing v6

| 元數據 | 值 |
|--------|-----|
| **版本** | v26.0523.1830 |
| **類型** | Indicator |
| **Pine Script** | v6 |
| **實體化時間** | 2026-05-23 18:30 CST |

## 核心邏輯

多時框擺動結構分析，同步顯示當前 TF 與 1H 的擺動高/低點與趨勢方向。內建 CHoCH 反轉偵測與流動性獵殺標記。

### 核心功能
- 擺動高/低點自動偵測（Pivot Left/Right）
- 多時框趨勢方向共識（Current TF + 1H MTF via `request.security`）
- CHoCH（Change of Character）反轉信號
- 流動性獵殺（Liquidity Sweep）標記 XY

### 使用方式
- 綠三角 = 擺動低點，紅三角 = 擺動高點
- 下方 Dashboard 顯示雙層趨勢方向
- 黃色 X 標記流動性掃蕩

## 參考來源
- JCO Swings Trend Multi TF, jcornierfra (GitHub)
- 經 TeleNexus Sovereign 主權化重寫