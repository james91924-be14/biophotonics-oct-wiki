---
title: "1045nm SS-PS-OCT 雙折射相位延遲與 k-clock 同步機制"
created: "2026-11-05"
updated: "2026-11-05"
category: "Signal-Processing"
sources:
  - "raw/2026-11-05-ps-oct-birefringence.md"
tags:
  - "ss-ps-oct"
  - "birefringence"
  - "1045nm"
  - "k-clock"
---

# 1045nm SS-PS-OCT 雙折射相位延遲與 k-clock 同步機制

## 1. 核心物理定義與機制

本實驗室使用中心波長 $\lambda_0 = 1045\text{ nm}$、掃頻速率 $200\text{ kHz}$ 之掃頻雷射（Swept-Source Laser）進行離體豬眼與後鞏膜（Posterior Sclera）生物組織成像。相較於傳統 $840\text{ nm}$ 波段容易受到視網膜色素上皮層（RPE）強烈散射，$1045\text{ nm}$ 近紅外光波段具備更佳的深層鞏膜穿透力。

光學同調斷層掃描之理論軸向解析度 $\delta z$ 定義為：

$$\delta z = \frac{2\ln 2}{\pi} \frac{\lambda_0^2}{\Delta\lambda}$$

系統透過雙通道平衡光電探測器（Balanced Photodetector, BPD）同步接收水平偏振通道 $E_H(z)$ 與垂直偏振通道 $E_V(z)$ 之干涉訊號。原始數據完成 k-space 線性插值與數值色散補償後，經快速傅立葉轉換（FFT）可由雙通道振幅比值求得深度方向之累積相位延遲（Cumulative Phase Retardation）：

$$\delta(z) = \arctan\left(\frac{|E_V(z)|}{|E_H(z)|}\right)$$

對累積相位延遲沿深度方向 $z$ 進行微分求取斜率，即可換算出後鞏膜膠原纖維之局部雙折射率（Local Birefringence）：

$$\Delta n = \frac{\lambda_0}{2\pi} \frac{d\delta(z)}{dz}$$

## 2. 實驗室系統參數對照

| 參數名稱 | 實驗室規範數值 | 備註說明 |
| :--- | :--- | :--- |
| 中心波長 ($\lambda_0$) | 1045 nm | 降低 RPE 散射，提升後鞏膜穿透深度 |
| 掃頻速率 | 200 kHz | 配合高速 DAQ 硬體觸發 |
| 頻譜半高寬 ($\Delta\lambda$) | [待實驗室實測補齊] | 原始筆記未提供，依防幻覺規範保留待補 |
| BPD 單臂參考光功率 | 0.5 mW ~ 1.0 mW | 防止平衡光電探測器飽和 |
| 樣品端入眼安全功率上限 | <= 1.8 mW | 遵循 ANSI Z136.1 規範，日常實驗設 1.2 ~ 1.5 mW |

## 3. 常見異常與排查關聯

- **橫向條紋偽影（Horizontal Stripe Artifacts）**：當 MATLAB 重建出的雙折射相位延遲圖出現嚴重橫向條紋偽影時，主因為掃頻雷射輸出之 k-clock 觸發訊號未與高速 DAQ 卡之 PFI0 時脈對齊，參見 [[k-clock-trigger]]。
- **B-scan 結構影像左右晃動錯位（Jitter）**：主因為 LabVIEW 掃描程式誤用軟體迴圈計時，必須改用硬體 Trigger 同步雙軸振鏡與 DAQ 卡，並預留 15% Flyback 緩衝點數，參見 [[galvo-daq-sync]]。
- **探測器飽和與雷射安全防護**：BPD 單臂參考光功率須維持於 0.5 mW 至 1.0 mW，樣品端功率須低於 1.8 mW，詳細光機防護規範參見 [[laser-safety-bpd]]。

## 4. 待驗證問題與參考來源

- **待補實驗數據**：需於暗房使用光譜分析儀（OSA）實測 1045nm 掃頻雷射之實際頻譜半高寬 $\Delta\lambda$，以補齊理論軸向解析度 $\delta z$ 計算值。
- **原始證據來源**：raw/2026-11-05-ps-oct-birefringence.md
