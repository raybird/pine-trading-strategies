# TnSovereignLaguerreRsiRegimeV6

> **TeleNexus Sovereign Trading Systems — Pine Script v6**
> Version: `v26.1121.0630` · Causal Audit: `2026-11-21 06:30 CST`

## 策略定位

**Laguerre RSI 低延遲體制策略**：以四階 Laguerre 全通 IIR 級聯取代固定週期
Wilder RSI。四階狀態 `L0..L3` 以 `nz(L[1], src)` 初始化，相鄰級差累加為
`cu/cd`，`LRSI = cu/(cu+cd)`（平坦市場回 0.5）。`gamma` 控制阻尼：低值反應
快、高值平滑。進場以 LRSI 穿越 0.2/0.8 為主證據，並要求 `L0>L1`（多）/
`L0<L1`（空）之級聯斜率確認，避免單純震盪誤判。

## 與現有庫之差異

- 全庫 `grep -ril "laguerre|ehlers" strategies/*.pine` **零命中**。
- 既有 `TnSovereignConnorsRsiV6` 使用 2 期 Wilder RSI，
  `TnSovereignRsiAtrV6` 使用固定週期 RSI，`TnSovereignSTCV6` /
  `TnSovereignStochV6` 使用隨機指標，`TnSovereignWaveTrendV20` 使用
  WaveTrend；本策略為**首例以 Laguerre 全通濾波器組重構 RSI**者，
  屬信號處理／低延遲維度。
- TradingView 當日可見 `Laguerre Pulse [Kiva]`（open-source），但受
  TradingView House Rules 約束；本移植改以明確 MIT 授權之 GitHub 原始檔
  為來源，符合歷次 OSS 規訓。

## 核心邏輯

```
ssrc = nz(src, src[1])
L0 = (1−γ)·ssrc + γ·nz(L0[1], ssrc)
L1 = −γ·L0 + nz(L0[1], ssrc) + γ·nz(L1[1], ssrc)
L2 = −γ·L1 + nz(L1[1], ssrc) + γ·nz(L2[1], ssrc)
L3 = −γ·L2 + nz(L2[1], ssrc) + γ·nz(L3[1], ssrc)

cu = Σ max(Li−Li+1, 0); cd = Σ max(Li+1−Li, 0)
LRSI = cu+cd > 0 ? cu/(cu+cd) : 0.5

long  = LRSI ×上穿 0.20 and L0 > L1 and daily EMA UP
short = LRSI ×下穿 0.80 and L0 < L1 and daily EMA DOWN (選配)
exit  = 2.0×ATR stop / 2.5R target / 1R BE / 8 根上限
```

日線 EMA200 取 `request.security(..., "1D", ..., lookahead_on)[1]`，
即前一根已收盤日線值，並要求 EMA 斜率同向；標的無效時 `na` → fail-closed。

## 主權化改造

| 項目 | 原作者（指標） | 主權版 |
|------|----------------|--------|
| 型別 | `indicator()`，無交易決策 | 自足 v6 `strategy()`，LRSI 穿越 + 級聯斜率為進場證據 |
| 風控 | 無 | ATR 2.0× 硬停損 + 2.5R 目標 + 1R 保本 + 8 根上限 |
| 部位 | 無 | 風險距離定倉 + 名目槓桿封頂 + `int` 落地 |
| 體制 | 無 | 日線 EMA200 方向與斜率雙閘門（前根已收盤值） |
| 流動性 | 無 | 選配 RVOL 下限 |
| 時間 | 無 | 時段 / 每日平倉 / 出場冷卻 / DD 守門 |
| 成交 | 不適用 | `process_orders_on_close=false` + `barstate.isconfirmed` |
| 宣稱 | 無 | 無（因果儀表板僅呈現狀態） |

## 非重繪契約

所有進場／出場訊號僅於已收盤 K 棒判定；日線序列一律取**前一根已收盤**
日線值並帶 `ignore_invalid_symbol = true`。時間出場使用
`immediately = true` 以貼近「收盤出場」語意。

## 資料合約

- Price：必要（OHLC）。Volume：僅 RVOL 開啟時需要。OI／參考標的：不需要。
- CFD-safe；合成 K 線（Heikin Ashi / Renko）之回測不保證有效。

## 來源

移植自 **mihakralj/pinescript**（MIT，Copyright 2025 Miha Kralj）
`indicators/oscillators/lrsi.pine`，branch `main`，commit
`0e91e5cfbcd5af47f0aa483fa86dcb0d5a7f471b`（`2026-03-01T01:11:38Z`，
`alignment w quantalib`）。本庫未經獨立回測驗證，不主張任何績效。
