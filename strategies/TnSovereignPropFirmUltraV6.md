# TnSovereignPropFirmUltraV6 — TeleNexus PropFirm 主權超防禦策略

## 策略概述
移植自 QuantAlgo 的 propfirm-ultra-strategy（thesenegalesehitch/Pine-Script），經 TeleNexus Sovereign 改造後，成為專為 PropFirm 挑戰賽設計的超防禦策略。整合 SMC/ICT 完整結構引擎與三層風控體系。

## 核心特性
- **PropFirm 三層防禦**: 日虧限額（$50）、全局回撤（$200）、連損暫停（3次），硬止損觸發時自動緊急平倉
- **SMC 結構引擎**: BOS/CHOCH/FVG/Order Block/Breaker Block/Inducement/Premium-Discount，完整 ICT 譜系
- **動態風險係數**: 根據市場體質（ADX/ATR/Vol）自動調整曝險，恢復模式降至 50%
- **主權評分系統**: 多維因果過濾 → 0-20 分置信度閾值，依市場體質自動調整門檻
- **Killzone 過濾**: 僅在倫敦（7-10 UTC）與紐約（13-16 UTC）開盤時段交易

## 模組說明
1. **市場體質檢測**: 6 種 RegimeType（STRONG_TREND / MILD_TREND / RANGING / HIGH_VOL / COMPRESSED / NEWS_SPIKE / DANGER）
2. **PropFirm 風控引擎**: 日虧餘額／全局回撤／連損計數／恢復模式／冷卻計數器
3. **動態風險因子**: 綜合 recovery 狀態、波動率、新聞脈衝、DD 深度後輸出 0.3-1.0 的風險係數
4. **雙 TP 執行**: TP1=1.5R（50% 倉位）、TP2=2.0-3.0R，觸發 TP1 後自動 Breakeven

## 參數建議
| 參數 | 建議值 | 說明 |
|------|--------|------|
| Max Daily Loss | $50 | PropFirm 日虧上限 |
| Risk % per Trade | 0.3-0.5% | 保守模式建議 0.3% |
| Pause after X Losses | 3 | 連損暫停保護 |
| Killzone Filter | true | 開啟時段過濾 |
| Min Score | 5-7 | 依市場波動調整 |

## 來源
- **原始倉庫**: thesenegalesehitch/Pine-Script
- **原始策略**: propfirm-ultra-strategy (v1.0.0, MIT License)
- **改寫紀錄**: 加入 TeleNexus enum 規訓、調整策略命名與 Dashboard、優化 score 計算、加入 cooldown 機制

## 版本號
v26.0528.1830