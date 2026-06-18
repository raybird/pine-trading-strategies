# TeleNexus IFVG + CISD Double Confirmation Strategy (v6)

**File:** `tn_ifvg_cisd_double_confirm_v6.pine`
**Version:** v26.0619.0630
**移植自:** [aleks-drozy/fyp-trading-strategy](https://github.com/aleks-drozy/fyp-trading-strategy) — Maynooth University FYP 2026

---

## 核心概念

本策略融合 **IFVG（Inverse Fair Value Gap）** 與 **CISD（Change in State of Delivery）** 兩種 ICT/SMC 結構分析工具，建立雙重確認入場模型。

### IFVG（反轉公平價值缺口）

- FVG 為三燭價格失衡區間，當價格貫穿該區間時形成 IFVG
- **看漲 IFVG**：價格從低處收盤高於下跌 FVG，意謂原有供應失衡已被需求推翻
- **看跌 IFVG**：價格從高處收盤低於上漲 FVG，意謂原有需求失衡已被供應推翻

### CISD（交付狀態變更）

- 追蹤市場結構的高低點回調
- 當價格突破先前結構高/低點時標記 CISD，代表市場方向性的結構轉變
- 相當於進階版的 CHoCH/BOS 偵測，但特別專注於回調高低的突破確認

### 雙重確認入場

交易僅在 **IFVG 方向與 CISD 狀態同向** 時觸發，附加流動性掃蕩過濾 + EMA 趨勢濾網。

---

## 參數說明

| 參數 | 預設值 | 說明 |
|------|--------|------|
| FVG Lookback | 3 | FVG 失衡偵測回溯 |
| FVG Threshold % | 0.0 | FVG 最小百分比門檻 |
| Swing Lookback | 8 | CISD 擺動高低點回溯 |
| EMA Length | 20 | EMA 趨勢濾網長度 |
| Use EMA Trend Filter | true | 啟用 EMA 方向過濾 |
| Sweep Lookback | 5 | 流動性掃蕩偵測回溯 |
| Use Sweep Filter | true | 啟用掃蕩過濾 |
| Use NY Session Only | false | 限紐約時段交易 |
| ATR Length | 14 | ATR 波動率計算 |
| Stop ATR Mult | 1.5 | 停損 ATR 倍數 |
| Risk Reward | 1.5 | 盈虧比 |

---

## 風險管理

- **停損**：ATR × Stop Mult，固定於入場價位
- **止盈**：ATR × Stop Mult × R:R
- **日交易上限**：每日最多 1 筆交易（防止過度交易）
- **流動性掃蕩過濾**：等效 1min sweep proxy，過濾假突破
- **EMA 趨勢濾網**：確保順勢交易

---

## 分類歸屬

市場結構與價格行為（Market Structure & Price Action）
