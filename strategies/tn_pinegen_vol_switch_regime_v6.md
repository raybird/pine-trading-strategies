# tn_pinegen_vol_switch_regime_v6 — PineGen Adaptive Volatility Regime Switch (Sovereign Port)

**版本**: v26.0604.1830 | **移植自**: PineGen-AI/adaptive-risk-regime-strategy

## 核心邏輯
ATR 波動體制偵測，低波動時執行均值回歸（反轉交易），高波動時執行突破追蹤（動量交易）。單一策略自適應兩種市場狀態。

## 主要功能
- **低波動模式**: 價格回到區間低/高時反向交易
- **高波動模式**: 價格突破區間時追蹤動量
- ATR 與其 SMA 比較判定體制
- 固定 R:R 風控（2.0）

## 參數
- ATR Length: 14
- Volatility Lookback: 50
- Range Length: 20
- Stop ATR Mult: 1.5
- Risk Reward: 2.0