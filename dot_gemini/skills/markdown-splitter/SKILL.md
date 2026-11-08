---
name: markdown-splitter
description: 此 Skill 專門用於處理長篇 Markdown 檔案（如超過 500~1000 行之架構書、專案文件或程式庫規劃），將其精準拆解為多份獨立、具模組化的 `.md` 檔案至指定目錄中，以便小模型（如 Gemini Flash）進行後續的單元派工（Sub-Agent Processing）。
license: MIT
---

## 核心工作流（Workflow）

1. **章節層級分析**：
   - 掃描目標 `.md` 檔案的標題標籤（Markdown Headings: `#` 或 `##`）。
   - 避免過度碎裂：預設以頂層 `#`（Level 1）或二級 `##`（Level 2）作為檔案切割邊界。
2. **無損文字切分（Lossless Extraction）**：
   - 嚴禁丟棄任何原始註解、程式碼區塊（Code Blocks）或 front-matter。
   - 保留程式碼區塊內部可能包含的 `#` 符號，不誤判為文件標題。
3. **檔名規範化（Normalization）**：
   - 檔名前綴加入兩位數序號（`01_`, `02_`, ...），保持檔案目錄排序一致性。
   - 清理不合法的檔名字元（過濾空白轉為底線、移除標點符號）。
4. **輸出目錄管理**：
   - 將切分後的檔案集中存放在指定資料夾（預設為 `<filename>_sections/`）。
   - 自動生成一份 `index.json`（Manifest 清單），記錄每個檔案的標題、檔名、行數範圍，利於後續 Orchestrator 進行任務派發。

## 執行腳本說明

內建執行腳本：`scripts/split_markdown.py`
