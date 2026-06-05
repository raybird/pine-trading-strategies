# tn_pinegen_lvn_reject_accept_v6 — PineGen LVN Rejection / Acceptance (Sovereign Port)

**版本**: v26.0604.1830 | **移植自**: PineGen-AI/lvn-rejection-acceptance-strategy

## 核心邏輯
使用 SMA 作為低量節點近似中心，ATR 波動頻帶建構動態區間。組合拒絕（回到頻帶內）與接受（站穩頻帶外）雙邏輯，相對成交量 <0.8 視為低參與。

## 主要功能
- SMA + ATR 頻帶：自適應市場波動
- 相對成交量過濾：減少高活動假信號
- 拒絕交易：價格短暫超出頻帶後回到內部
- 接受交易：價格站穩頻帶外持續方向
- ATR 風控 + 固定 R:R 2.0

## 參數
- LVN Detection Length: 40
- ATR Length: 14
- LVN Width (ATR mult): 0.8
- Stop ATR Mult: 1.5
- Risk Reward: 2.0