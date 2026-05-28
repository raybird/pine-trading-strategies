# TnSovereignVeinReversalV6

**版號：** v26.0529.0630  
**分類：** Market Structure & Price Action / Reversal  
**核心概念：** 前視型反轉品質分級 + 主權趨勢濾網

---

## 策略哲學

市場反轉並非隨機事件 — 每一次反轉都帶有可量測的品質特徵，包括**反轉速度**、**最大不利波動 (MAE)**、與**波動率足跡**。本策略將每一個潛在反轉標記為 4 級品質（+2/+1/-1/-2），僅對最高級別（+2/-2）執行交易，並疊加 TeleNexus 主權過濾層。

## 核心邏輯

### 1. 反轉品質分級
- **前瞻窗口評估：** 在當前 K 線結束後，向前掃描 forwardBars（弱目標）和 extendedBars（強目標）
- **目標達成條件：** 價格必須在指定窗口內達到 targetATR×（弱）或 strongATR×（強）
- **最大不利限制：** 允許的最大回撤為 maxAdverseATR×，超過則視為失敗
- **分級規則：**
  - +2/−2（強反轉）：達成強目標 或 在 fastBarsThresh 內快速達成弱目標且 MAE ≤ 門檻
  - +1/−1（弱反轉）：僅達成弱目標，未達強化條件

### 2. 主權趨勢濾網 (Sovereign Regime Filter)
- **VWAP 斜率判斷長期方向**
- **EMA 14/28 交叉確認短期趨勢**
- 僅允許牛市信號在上升趨勢中交易，熊市信號在下降趨勢中交易
- 盤整市場（無明確趨勢方向）自動過濾所有信號

### 3. 風險管理
- **ATR 動態倉位：** 止損 = ATR × slMult，止盈 = ATR × tpMult
- **保本機制：** 浮盈達到 beTrigR× 時自動將止損移至開倉價
- **冷卻期：** 出場後可設定 cooldown 根 K 線不交易

## 輸入參數

| 群組 | 參數 | 預設值 | 說明 |
|------|------|--------|------|
| Labeling | atrLen | 14 | ATR 計算週期 |
| Labeling | forwardBars | 8 | 弱目標掃描窗口 |
| Labeling | extendedBars | 16 | 強目標掃描窗口 |
| Labeling | targetATR | 1.5 | 弱目標倍數 |
| Labeling | strongATR | 2.5 | 強目標倍數 |
| Labeling | maxAdverseATR | 0.6 | 最大回撤限制 |
| Quality | fastBarsThresh | 4 | 快速反轉門檻 |
| Quality | maeStrongThresh | 0.3 | 強反轉 MAE 門檻 |
| Cluster | minGapBars | 3 | 同向標記最小間隔 |
| Signal | tradeLongStrong | true | 交易強牛市信號 |
| Signal | tradeShortStrong | true | 交易強熊市信號 |
| Risk | slMult | 1.5 | 止損 ATR 倍數 |
| Risk | tpMult | 3.0 | 止盈 ATR 倍數 |
| Break-Even | enableBE | true | 啟用保本停損 |
| Break-Even | beTrigR | 1.0 | 保本觸發 R 倍數 |
| Strategy | dirMode | Both | 交易方向 |
| Strategy | cooldown | 3 | 出場冷卻 K 線數 |

## 因果審計表

策略右上角嵌入即時狀態面板：

| 欄位 | 值 | 說明 |
|------|-----|------|
| TnVeinRevV6 | v26.0529.0630 | 策略名稱與版號 |
| Causal | BULL/BEAR/NEUTRAL | 當前 VWAP 斜率方向 |
| Regime | LOCKED/CHOP | 趨勢鎖定狀態 |
| ATR | #.## | 當前波動率數值 |

## 資料來源

本策略靈感來自 [WavesUnchained Vein Reversal Labeler](https://github.com/casoon/pine-scripts)（casoon/pine-scripts），經 TeleNexus Sovereign 改造加入因果審計、趨勢濾網與主權風險管理層。

## 相依性

- Pine Script v6
- 無外部函式庫依賴