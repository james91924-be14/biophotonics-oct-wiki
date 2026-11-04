# AGENTS.md — BioPhotonics & OCT Lab Wiki 專案員工手冊

每次開始工作前，請務必完整閱讀本文件。本文件定義了「生醫光電實驗室知識庫與互動講義系統」的目錄架構、格式標準、修改限制與驗收條件。不要猜測未寫明的規則；若有原始資料不足之處，請先列出缺漏清單詢問人類研究者。

---

## 1. 專案目的與定位
本專案旨在解決生醫光電實驗室（專注於 1045nm 200kHz SS-PS-OCT 掃頻偏振敏感光學同調斷層掃描、GRIN 內視鏡微探頭與 LabVIEW 高速硬體同步）之文獻沉澱與學長姐技術交接問題。
系統結合 Karpathy 的 LLM Wiki 模式與單檔 HTML 互動講義架構，將零散的實驗紀錄與論文轉化為「結構化 Markdown 知識節點」與「可直接在瀏覽器翻頁閱讀的教學網頁」。

---

## 2. 要什麼成品：目錄結構與命名規範 (Deliverables & Architecture)

專案根目錄結構固定如下，AI 新增內容時必須嚴格放置於對應路徑：

```text
/
├── AGENTS.md                        # 本員工手冊（唯讀規則檔，未經指示不得覆寫）
├── index.html                       # 公開入口網站首頁（收錄所有 HTML 講義卡片與 Wiki 索引）
├── log.md                           # 知識庫自動化維護日誌（每次操作必更新）
├── raw/                             # 原始素材區（存放人類提供的論文摘要、實驗數據或原始筆記）
│   └── YYYY-MM-DD-<topic-slug>.md
├── wiki/                            # 結構化知識庫（由 AI 從 raw/ 萃取生成之 Markdown 概念頁）
│   └── <concept-slug>.md
└── lessons/                         # 互動式教學網頁區（供瀏覽器直接開啟之單檔 HTML 講義）
    └── NN-<lesson-slug>.html
