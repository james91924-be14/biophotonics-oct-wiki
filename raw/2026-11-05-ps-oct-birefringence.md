# 原始實驗筆記：1045nm SS-PS-OCT 雙折射相位延遲與 k-clock 同步機制

- 紀錄日期：2026-11-05
- 紀錄人員：許浩哲
- 權限狀態：唯讀原始證據檔 (Immutable Raw Source)

## 原始內容
1. 系統光源與用途：我們實驗室使用中心波長 1045 nm、掃頻速率 200 kHz 的掃頻雷射（Swept-Source Laser）進行離體豬眼與後鞏膜（Posterior Sclera）成像。因為傳統 840 nm 容易被視網膜色素上皮層（RPE）散射，1045 nm 能提供更好的深層鞏膜穿透力。理論軸向解析度公式為 \delta z = \frac{2\ln 2}{\pi} \frac{\lambda_0^2}{\Delta\lambda}（目前這台雷射的實際頻譜半高寬 \Delta\lambda 數值我手邊沒記到，請先依規則標註待補齊）。
2. 偏振雙折射計算：系統透過平衡光電探測器（BPD，單臂參考光功率須控制在 0.5 mW 到 1.0 mW）同步接收水平通道 E_H(z) 與垂直通道 E_V(z) 訊號。做完 k-space 線性插值與色散補償後，經 FFT 可算累積相位延遲 \delta(z) = \arctan(|E_V(z)| / |E_H(z)|)，再對深度微分求斜率就能算出局部雙折射率 \Delta n = \frac{\lambda_0}{2\pi} \frac{d\delta(z)}{dz}。
3. 常見異常排查：如果 MATLAB 算出的相位圖出現嚴重橫向條紋偽影，通常是掃頻雷射的 k-clock 觸發訊號沒有跟高速 DAQ 卡的 PFI0 時脈對齊（可關聯至 [[k-clock-trigger]]）；如果 B-scan 影像左右晃動錯位（Jitter），則是 LabVIEW 誤用軟體迴圈計時，必須改用硬體 Trigger 並預留 15% Flyback 緩衝點數（可關聯至 [[galvo-daq-sync]]）。另外樣品端入眼功率依 ANSI Z136.1 規定不得超過 1.8 mW（日常實驗設 1.2 到 1.5 mW，關聯至 [[laser-safety-bpd]]）。
