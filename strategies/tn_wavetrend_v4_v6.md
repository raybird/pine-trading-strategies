# tn_wavetrend_v4_v6 (v26.0531.0630)

> **「波動趨勢 v4 — 主權品質閘門下的動量反轉」**

## 1. 策略概述
本策略是 **WaveTrend v4** 動量振盪指標的主權化移植，保留經典的 WaveTrend 核心算理，並疊加 TeleNexus 品質閘門與多時框 OS/OB 設定。目標是在超買/超賣極值區捕捉 wt1/wt2 交叉反轉信號。

## 2. 來源歸屬
- **Port of WaveTrend v4 by WavesUnchained (casoon/pine-scripts)**
- 原始來源：https://github.com/casoon/pine-scripts
- 核心算理：WavesUnchained 開發的經典 WaveTrend 動量振盪器

## 3. WaveTrend 振盪器力學
WaveTrend 核心計算路徑：
1. **esa** = ema(hlc3, chLen) — 平滑均衡線
2. **d** = ema(|hlc3 - esa|, chLen) — 平均絕對偏差
3. **ci** = (hlc3 - esa) / (0.015 × d) — 歸一化偏離指標
4. **wt1** = ema(ci, avgLen) — 主振盪線
5. **wt2** = sma(wt1, sigLen) — 訊號觸發線

## 4. 多時框 OS/OB 入場邏輯
策略根據當前圖表時框自動選取對應的 OS/OB 閾值：

| 時框 | OB | OS |
|------|----|----|
| 15m  | 60 | -60 |
| 1H   | 53 | -53 |
| 4H   | 50 | -50 |
| 1D   | 45 | -45 |

**入場條件：**
- **LONG**：wt1 上穿 wt2，且 wt1 低於該時框 OS 值
- **SHORT**：wt1 下穿 wt2，且 wt1 高於該時框 OB 值

### 品質閘門
| 閘門 | 名稱 | 功能 |
|------|------|------|
| Gate A | ATR Rank Band Killer | 當 ATR 百分位排名 ≥ 70 時抑制入場（高波動 regime 過濾） |
| Gate C | HTF Exhaustion Filter | 檢查高時框 WT 是否處於極端區（衰竭上下文） |
| Gate G | Counter-Trend Range Filter | 當 K 線範圍超過 20 期 SMA 的 1.5 倍時阻擋逆勢信號 |

## 5. 風險管理框架
- **止損 (SL)**：1.5× ATR，動態計算
- **止盈 (TP)**：3.0× ATR，固定 R:R = 1:2
- **冷卻機制**：出場後等待 N 根 K 線方可再次入場
- **會話過濾**：可限定交易時段
- **方向模式**：Both / Long Only / Short Only

## 6. 推薦配置
| 參數 | 預設值 | 說明 |
|------|--------|------|
| chLen | 10 | 通道長度（敏感度） |
| avgLen | 21 | 平均長度（平滑度） |
| sigLen | 4 | 訊號線長度 |
| ATR SL | 1.5× | 止損倍數 |
| ATR TP | 3.0× | 止盈倍數 |
| 時框 | 1H / 4H | 最適運行時框 |
| 標的 | BTCUSDT, ETHUSDT, NAS100 | 流動性高的交易對 |

---
*Calibrated at 2026-05-31 06:30 (CST) | Version: v26.0531.0630 | Calibration: Sovereign*