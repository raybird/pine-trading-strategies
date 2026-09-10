# TnSovereignOscDivZonesV6 — TeleNexus 振盪器背離區間主權策略

> **分類**: Mean Reversion & Oscillator / Divergence  
> **版號**: v26.0910.1830  
> **獵頭源**: casoon/pine-scripts (WavesUnchained) Oscillator Divergence Zones v1.2.2  
> **狀態**: 已實體化

---

## 策略概述

以 **RSI / CCI / MFI** 三振盪器各自的「動態統計區間 (Dynamic Zones)」進行背離獵取。核心差異於一般背離畫線 —— 本策略要求背離**必須發生於振盪器的 3σ 統計外緣之外**，且由 ATR 自適伸縮區寬，最後以三振盪器「同向一致」聚合計數與 200 EMA 趨勢地板把關。

## TeleNexus Sovereign 強化

| 項目 | 原始 | 強化後 |
|------|------|--------|
| 區間 | STDEV 固定 σ | 加入 ATR 自適伸縮（ATR × scale 疊加） |
| 聚合 | 單一振盪器 | RSI/CCI/MFI 三引擎 convergence ≥ min（可 1~3） |
| 濾網 | 無 | 200 EMA 趨勢 + ATR corridor（排除壓縮/尖峰） |
| 風控 | 固定 SL/TP | 0.75R~1.5R bracket + Trailing + 防重複鎖 |

## 核心邏輯

1. **Dynamic Zone** — `close` 的 SMA ± ZDEV×STDEV，若 `useAtrAdaptive` 再疊加 `ATR×atrScale`
2. **Divergence** — pivot 比對：price HH + 振盪器 LH（多）、price LL + 振盪器 HL（空）
3. **Zone Crossing** — 收盤穿越 zone 外緣才成立訊號（非重繪契）
4. **Convergence** — RSI+CCI+MFI 同向背離計數達 `minConvergence` 門檻
5. **Filter** — 200 EMA 順勢地板 + ATR corridor 排除亂流

## 參數建議

| 參數 | 預設 | 說明 |
|------|------|------|
| Zone Deviation | 3.0 | STDEV 倍數 |
| Zone Width | 8 | 統計窗口 |
| Oscillator Length | 14 | RSI/CCI/MFI 共同長度 |
| Min Convergence | 1 | 同向振盪器最低數 |
| ATR Scale | 1.5 | 自適區寬強度 |
| SL / TP | 50 / 100 | 點數 bracket |

## 風險

- 三振盪器全開時訊號極稀少（convergence=3）
- Zone 過寬（高偏差）時穿越確認延遲
- 適合區間市場；強趨勢中背離反轉易失效，建議搭配趨勢濾網