# TnSovereignOrbMultiSessionV6

**版號：** v26.0529.0630  
**分類：** Volatility & Breakout / 多時段 ORB  
**核心概念：** 多交易時段開盤區間突破引擎 + 主權趨勢閘門

---

## 策略哲學

開盤區間突破 (ORB) 是日內交易中機率最高的設定之一。**關鍵在於時段** — 亞洲、倫敦、紐約三大交易時段的開盤區間各自蘊含不同的機構訂單流特徵。本策略自動偵測當前時段，捕捉該時段初始 ORB 的突破方向，並疊加 VWAP 趨勢閘門與成交量確認。

## 核心邏輯

### 1. 多時段偵測
- 支援三大交易時段獨立設定（HHMM 格式）
- 在時段切換時自動重置 ORB 區間
- 當前活躍時段顯示於因果審計表

### 2. 開盤區間計算
- 從時段起點開始累積最高/最低價
- ORB 區間長度可設定（預設 60 分鐘）
- 突破閾值 = ORB 高/低 ± ATR × breakoutMult

### 3. 主權確認閘門
- **VWAP 趨勢閘門：** 多頭突破需價格在 VWAP 之上，空頭反之
- **成交量確認：** 可選的相對成交量門檻（relVol ≥ minRelVol）
- 僅在兩者同時滿足時執行交易

### 4. 風險管理
- 止損：ORB 區間對側 ± ATR × 0.5
- 止盈：ATR × 2.0（可調整）
- 最大持倉 K 線數保護

## 輸入參數

| 群組 | 參數 | 預設值 | 說明 |
|------|------|--------|------|
| Session Times | asiaStart/End | 0000-0900 | 亞洲時段 |
| Session Times | londonStart/End | 0800-1630 | 倫敦時段 |
| Session Times | nyStart/End | 1330-2100 | 紐約時段 |
| ORB | orbLen | 60 | ORB 區間長度（分鐘） |
| ORB | breakoutMult | 0.5 | 突破 ATR 倍數閾值 |
| ORB | requireVol | true | 要求成交量確認 |
| ORB | minRelVol | 1.5 | 最小相對成交量 |
| ORB | useVwapGate | true | 啟用 VWAP 趨勢閘門 |
| Risk | maxHoldBars | 48 | 最大持倉 K 線數 |

## 因果審計表

| 欄位 | 值 | 說明 |
|------|-----|------|
| ORBMultiSession | v26.0529.0630 | 版號 |
| Session | ASIA/LONDON/NY | 當前活躍時段 |
| Vol | #.## | 當前相對成交量 |
| ATR | #.## | 當前波動率 |

## 資料來源

靈感來自 [ORB Multi-Model Indicator](https://github.com/BobLeeHacker/ORB-Multi-Model-Indicator)（BobLeeHacker），經 TeleNexus Sovereign 改造加入多時段架構、VWAP 閘門與主權風險管理。

## 相依性

- Pine Script v6
- 無外部函式庫依賴