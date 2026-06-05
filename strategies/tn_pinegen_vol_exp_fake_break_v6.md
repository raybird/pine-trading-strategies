# tn_pinegen_vol_exp_fake_break_v6 — PineGen Vol Expansion + Fake Breakout (Sovereign Port)

**版本**: v26.0604.1830 | **移植自**: PineGen-AI/volatility-expansion-fake-breakout-strategy

## 核心邏輯
監測 ATR 波動擴張（atr > avg * 1.3），結合範圍突破 + 蠟燭強度過濾來避免假突破陷阱。僅在波動擴張、價格突破範圍、且有強力收盤確認時進場。

## 主要功能
- **波動擴張偵測**: ATR 突破其 SMA 的 1.3 倍閾值
- **範圍突破**: 價格突破 rolling range H/L
- **假突破過濾**: 蠟燭必須在突破方向強力收盤
- 僅在高動量環境交易，避免低品質信號
- ATR 風控 + 固定 R:R 2.0

## 參數
- Range Lookback: 20
- ATR Length: 14
- Vol Expansion Mult: 1.3
- Stop ATR Mult: 1.5
- Risk Reward: 2.0