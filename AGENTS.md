# AGENTS.md — NYCU BioPhotonics & OCT Lab Wiki 專案員工手冊 (v2.0)

每次開始工作前，請務必完整閱讀本文件。本文件定義了「生醫光電實驗室互動學習網與 LLM Wiki 知識庫」的目錄架構、6 大知識分類、視覺互動規範、防幻覺限制與五步驗收條件。

---

## 1. 專案目的與定位
本專案旨在將生醫光電實驗室（涵蓋 OCT 基礎干涉原理、1045nm 200kHz SS-PS-OCT 雙折射成像、GRIN 微探頭與 OpenSCAD 光機建模、LabVIEW 高速 DAQ 同步、BPD 訊號重建、CNN 散斑降噪與雷射環安衛）之研究資產，轉化為**初學者友善的互動式科普學習網站**與**結構化 LLM Wiki 知識庫**。

---

## 2. 要什麼成品：目錄結構與 6 大知識分類 (Architecture & Taxonomy)

專案根目錄結構固定如下：
- `AGENTS.md`：本員工手冊（唯讀規則檔，定義全站擴充標準）。
- `index.html`：互動式學習入口首頁（內建 8 大主題卡片、分類篩選器、關鍵字搜尋、OCT 解析度模擬器、Mochi 翻翻卡、學習進度追蹤與 Wiki 線上閱讀視窗）。
- `log.md`：知識庫自動化維護日誌（每次新增或修改必更新）。
- `raw/`：唯讀原始素材區（存放實驗紀錄或文獻摘要，命名格式 `YYYY-MM-DD-<slug>.md`）。
- `wiki/`：結構化 Markdown 知識節點（命名格式 `<concept-slug>.md`）。
- `lessons/`：單檔獨立（Standalone Single-File）之投影片式互動講義（命名格式 `NN-<lesson-slug>.html`）。

### 6 大知識分類標籤 (Categories)
1. `Optics-101`：基礎光學與麥克森低同調干涉原理
2. `SS-PS-OCT`：1045nm 掃頻雷射與後鞏膜偏振雙折射系統
3. `Micro-Optics`：GRIN 梯度折射率微探頭與 OpenSCAD 3D 列印光機
4. `Hardware-Sync`：LabVIEW 雙軸振鏡與高速 DAQ 硬體時脈同步
5. `Signal-AI`：BPD 差動訊號處理、FFT 重建與深度學習散斑降噪
6. `Safety-Agent`：Class 3B 雷射環安衛規範與 Agentic AI 自動化工作流

---

## 3. 網頁視覺風格與互動功能規範 (UI/UX & Interactive Standards)

1. **雙主題視覺系統（Warm Ivory & Dark Optics Lab）**：
   - 預設採用啟發學習動機的「暖陽米白學術風（`#FAF7F2` 背景、白底毛玻璃卡片、珊瑚橘 `#EA580C` 與青藍 `#0284C7` 強調色）」，並支援一鍵切換為「光學暗房深色模式（`#0B0F17`）」。
2. **四大互動學習元件**：
   - **分類篩選與即時搜尋**：首頁卡片必須綁定 `data-cat` 屬性，支援標籤切換與關鍵字即時過濾。
   - **動手玩光學模擬器**：內建中心波長 $\lambda_0$、頻寬 $\Delta\lambda$ 與入眼功率 $P$ 滑桿，即時計算軸向解析度 $\delta z$ 並檢核 ANSI Z136.1 (1.8 mW) 安全上限。
   - **新手快問快答翻翻卡 (Flashcards)**：支援點擊翻面查看實驗室常見除錯 QA。
   - **數學公式渲染**：全面載入 KaTeX CDN 渲染 LaTeX 公式。

---

## 4. 有什麼限制：AI 操作邊界與防幻覺守則 (Constraints)

1. **禁止竄改原始資料**：`raw/` 資料夾內檔案視為不可變（Immutable）之原始實驗證據，嚴禁修改或刪除。
2. **禁止物理參數幻覺**：所有寫入 `wiki/` 與網頁的實驗室規格，必須 100% 來自原始筆記。若缺乏實測數值（如特定雷射頻譜半高寬 $\Delta\lambda$ 或角膜光斑直徑 $d$），強制標註為 `[待實驗室實測補齊]`，嚴禁自行編造數據。
3. **禁止破壞既有版面與互動腳本**：擴充 `index.html` 時，僅能於 `#lessonsGrid`、`modalData` 與 Wiki 總覽表中新增項目並更新統計數字，不得刪除既有功能區塊。

---

## 5. 怎麼算做完：五步標準作業流程 (Ingest-to-Publish Pipeline)

當人類交辦新增主題時，AI 必須依序完成以下五步並勾選驗收表：
1. **Step 1 (Save Raw)**：將原始筆記存入 `raw/YYYY-MM-DD-<slug>.md`。
2. **Step 2 (Compile Wiki)**：建立或更新 `wiki/<slug>.md`（含 YAML 標頭、公式、參數表與 `[[雙向連結]]`）。
3. **Step 3 (Build Lesson)**：生成單檔互動講義 `lessons/NN-<slug>.html` 或註冊至首頁 `modalData` 閱讀器。
4. **Step 4 (Sync Index)**：於 `index.html` 新增課程卡片、更新完成度統計與 Wiki 對照表。
5. **Step 5 (Log Activity)**：於 `log.md` 頂部新增一筆 `[YYYY-MM-DD] [PUBLISH]` 異動紀錄。
