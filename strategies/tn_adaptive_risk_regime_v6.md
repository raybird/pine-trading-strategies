# tn_adaptive_risk_regime_v6 (v26.0530.0630)

> **「波動率並非噪音——它是市場的呼吸節奏。適應它，而非對抗它。」**

## 1. 核心精髓
本策略實現了 **波動率體制自適應交易模型**，源自 PineGen-AI 的 Adaptive Risk Regime Strategy，經 TeleNexus 主權審計重鑄。核心洞察是：市場在低波動時期表現為區間震盪（均值回歸），在高波動時期表現為趨勢動能（突破跟隨）。本策略自動檢測當前波動率體制，並切換對應的交易邏輯。

## 2. 雙重體制規訓
- **Low Vol Regime (低波動 — 均值回歸)**: 當 ATR 低於其 SMA 均值時，市場處於壓縮狀態。策略執行區間極限反轉交易（Range Fade），在區間邊界反向介入。
- **High Vol Regime (高波動 — 突破跟隨)**: 當 ATR 高於其 SMA 均值時，波動率釋放。策略執行區間突破跟隨交易（Breakout Momentum），在價格確認突破區間後順勢介入。

## 3. 預期性能
- **環境**: 1H / 4H / D（全市場適用，特別適合 ETF、指數與主流加密貨幣）
- **特徵**: 體制切換機制使策略能在不同市場階段維持競爭力，避免單一策略在特定市場條件下失效
- **風險管理**: 低波動時保守 R:R (1:2)，高波動時積極 R:R (1:3)，動態匹配市場波動特徵

## 4. 規訓記錄
- **v26.0530.0630**: 首版實體化。移植自 PineGen-AI adaptive-risk-regime-strategy。實裝 Sovereign 體制自適應 HUD 與雙重風險模型。

---
*Calibrated at Sat May 30 06:30:31 CST 2026 | Calibration: Sovereign*