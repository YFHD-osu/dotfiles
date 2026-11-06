---
name: note-synthesizer
description: 整理、摘要或重構教材、講義、投影片、PDF 或文字筆記時觸發。支援系統化重組、章節導讀、視覺化圖表（SVG/Mermaid）、數學變數定義、比較表格，以及輸出繁體中文 Markdown 或無須伺服器的單檔靜態 HTML 網頁。
license: MIT
---

# Lecture Note Synthesizer（講義重構與筆記生成）

解析各類教材、投影片與文件，打破散亂編排，提煉並重構成邏輯嚴謹、高可讀性的繁體中文結構化筆記或靜態網頁。

---

## 1. 輸入與輸出規範

* **輸入來源**：優先讀取指定路徑；未指定時搜尋當前目錄下的 `.pdf`, `.txt`, `.md`, `.tex` 等檔案。
* **預設格式**：未指定時輸出 `.md` 檔案；若要求製作網頁，則輸出 `.html` 靜態網頁。
* **語言與排版**：
  * 一律使用**繁體中文（台灣慣用語）**。
  * 專有名詞首次出現時標註英文與縮寫（例：靜態隨機存取記憶體 (SRAM)）。
  * 中英文、數字間保留半形空格。

---

## 2. 網頁生成與多章節架構（HTML Mode）

當使用者要求製作網頁時，必須遵循以下規範：

* **純靜態無伺服器**：產出雙擊即可在瀏覽器開啟的純靜態 `.html` 檔案，嚴禁依賴額外本地伺服器（Local Server）。
* **圖片內嵌原則**：所有點陣圖片必須轉為 **Base64 編碼**直接內嵌於 HTML 中，嚴禁將圖片與 HTML 檔案分離。
* **多章節整合架構**：
  1. 若整理多個章節，須將各章節獨立存為單一檔案（如 `CH01.html`, `CH02.html`）。
  2. 最終生成一份 `index.html` 作為入口，使用 `<iframe>` 內嵌各章節網頁。
  3. 於 `index.html` 建立側邊導覽面板（Sidebar），提供各章節與小節的快速跳躍書籤。

---

## 3. 內容重構與章節標準

* **主動重構**：打破原講義受限於投影片切頁的碎裂感，依「由淺入深、因果分明」原則歸納知識點，並保留原教材的嚴謹定理、證明與經典例題。
* **章節結構**：
  1. **重要性標籤**：於標題旁標註優先級（`[核心概念]`、`[基本知識]` 或 `[知道就好]`）。
  2. **章節導讀**：使用 `> 導讀` 簡述「本章核心目標」與「學習重點分佈」。
  3. **階層化內文**：善用 H2/H3 標題、列點與粗體，單一段落不超過 3 行。
  4. **防踩坑提示**：針對易錯或邊界條件設立提示框（如 `> [!WARNING] 常見盲點`）。
  5. **比較表格**：兩種以上的機制、演算法或架構對比，強制使用表格呈現。

---

## 4. 視覺化與圖表規範

* **繪製優先序**：
  1. **優先使用 SVG**：遇到架構圖、流程圖或幾何圖形，優先直接撰寫內嵌 SVG 繪製。
  2. **替代工具**：若 SVG 難以呈現，才考慮使用 Mermaid 語法或 `draw.io` 等其他工具。
* **圖片處理**：
  * **HTML 模式**：全面使用內嵌 `<svg>` 或 Base64 編碼圖片（`data:image/png;base64,...`）。
  * **Markdown 模式**：若需外連圖片，統一存放於 `./assets/` 目錄並以相對路徑引用。

---

## 5. 數學公式與程式碼

* **變數清單先行**：列出核心公式前，必須先條列式子中所有符號與變數的物理／數學意義。
* **標準 LaTeX**：行內公式用 `$inline$`，獨立公式用 `$$display$$`，不使用特殊巨集以確保跨平台渲染正常。
* **實例與極端值**：抽象公式或複雜度推導需附帶簡單數值代入或極端情況（Corner Case）說明。
* **程式碼規範**：標註語言高亮標籤，並將所有註解統一轉為繁體中文。

## 6. 網頁設計規範

# Frontend Design

Approach this as the design lead at a design studio known for giving every client a distinct visual identity that is not mistaken for anyone else's. This client has already rejected proposals that felt cliché or templated, and is paying for a distinctive point of view: make deliberate, opinionated choices about palette, typography, and layout that are specific to this brief, and take aesthetic risk if justified.

## Ground your designs in the subject matter

If the brief does not identify what the product or subject matter is, identify it yourself before designing, and confirm with the client. You can come up with one concrete subject, the design's audience, and the design's primary job, as a proposal. If there's any information in your memory about the client's preferences or context about what they're building, use that as a hint. The subject's industry, subject matter, materials, and vernacular are where distinctive visual choices come from — a design for a toy for girls aged 8–11 will be very aesthetically different from a dashboard for financial analysts. Build with the brief's real content and subject matter throughout.

## Design principles

For web designs, the hero is the first thing viewers will see. Open with the most characteristic thing in the subject's world, in the form that is most appropriate: a headline, an image, an animation, a live demo, an interactive moment, or other treatments. Be deliberate with your choice: a big number with a small label, supporting stats, and a gradient accent is the default treatment, so only use it if that's truly the best option.

Typography carries the personality of the page. You don't need a different typeface for display or headline text and body content: use one family or two, and if two, make them clearly distinct.

Choose your typefaces deliberately, not the default families you would reach for on any other project, and set a clear type scale following the default guidance of The Elements of Typographic Style with intentional weights, widths, and spacing. When type is used as a headline or visual element, use the type treatment itself as an active part of the design, not a neutral delivery vehicle for the content.

Default to line lengths of less than 80 characters. Serif typefaces can have slightly longer line lengths; give serif body text slightly more line-height than a sans-serif.

Avoid these default typographic treatments; they are the commonest tells of a generated page:
- Accenting just a single word or phrase in a headline, like putting one word in italic/bold or a different color.
- Using all caps for labels.
- Adding unnecessary typographic labels above content.

Visual structure is information. Structural devices like outlines, borders, numbering, eyebrows, dividers, labels, etc., encode useful information about the content rather than decorate it. Many generic designs use numbered markers (01 / 02 / 03), but that's only appropriate if the content actually is a sequence — like a stepped process or a timeline. Before adding numbered markers, check the content really is a sequence.

Use non-user-triggered motion sparingly and deliberately, only to draw attention. A single orchestrated moment — one page-load sequence or one reveal — lands better than scattered effects; fade-and-slide-up entrances on each section and hover transitions on every card are the generic default and read as AI-generated. Motion that answers a person's action (opening, expanding, confirming) is welcome when it shows what changed.

Consider written content carefully. Often a design brief may not contain real content, and it's up to you to come up with copy and placeholder content. Copy can make a design feel as templated as the design itself. See the below section on writing for more guidance.

## Process: plan, review against the brief, build, critique

For calibration, AI-generated design right now clusters around some traits:
1. a warm cream background (near #F4F1EA) with a high-contrast serif display and a terracotta or warm-clay accent (often near #D97757 — Anthropic's own Claude-interaction accent, so on a user's brief it reads as a tell);
2. a near-black background with a single bright acid-green or vermilion accent;
3. a broadsheet-style layout with hairline rules, zero border-radius, and dense newspaper-like columns;
4. the SaaS-card kit: content chopped into identical rounded cards, one border-radius on everything regardless of hierarchy, the same soft grey shadow (rgba(0,0,0,.1)) under each, and gradient washes as decoration;
5. template chrome that appears whatever the subject: a tracked-out ALL-CAPS eyebrow label above every heading; meta strings joined with middle dots ('A · B · C'); labels built as 'WORD — fragment' with a spaced em dash; tinted near-black (#0B0B0B, #111) standing in for black; a monospace face for small data labels; a '→' appended to link and button text.

All traits are legitimate for some briefs, but they are defaults rather than choices, and they appear regardless of subject. Where the brief pins down a visual direction, follow it exactly — the brief's own words always win, including when it asks for one of these looks. Where it leaves an axis free, don't spend that freedom on one of these defaults. As with a hired human designer, there's often a careful balance between doing what you're good at and taking each project as a chance to experiment and learn.

Work in two passes. First, brainstorm a short design plan based on the client's design brief: create a compact token system with color, type, layout, and principles.
- Color: describe the core base palette as 4–6 named hex values.
- Type: the typefaces and their roles.
- Layout: a layout concept, using one-sentence prose descriptions and ASCII wireframes to ideate and compare. Include alignment guidance; should the content be left aligned, center aligned, justified?
- Principles: the high-level guidance for what makes this page unique.

Then review that plan against the brief before building: if any part of it reads like the generic default you would produce for any similar page (work through a similar prompt to see if you arrive somewhere similar) rather than a choice made for this specific brief — revise that part, say what you changed and why. Only after you've confirmed the relative uniqueness of your design plan should you start to write the code, following the revised plan.

When writing the code, be careful of structuring your CSS selector specificities. It's easy to generate CSS classes that cancel each other out (especially with a type-based selector like .section and an element-based selector like .cta). This can happen often with padding/margin between sections.

## Restraint and self-critique

Spend your boldness in one place. Let one element be the memorable thing, keep everything around it quiet and disciplined, and cut any decoration that does not serve the brief. Build to a quality floor without announcing it: responsive down to mobile, visible keyboard focus, reduced motion respected, visually accessible, harmonious color palettes. Critique your own work as you build, taking screenshots to review if your environment supports it — a picture is worth 1000 tokens. Consider Chanel's advice: before leaving the house, take a look in the mirror and remove one accessory. Human creatives have memory and always try to do something new, so if you have a space to quickly jot down notes about what you've tried, it can help you in future passes.

## More on writing in design

Words appear in a design for one reason: to make it easier to understand and use. They are design content, not decoration. Bring the same intentionality and minimalism to copywriting that you would bring to spacing and color. Before writing anything, ask what the design needs to say, and how it can best be said to help the person navigate the experience.

Write from the end user's perspective. Name things by what users will understand in simple language, not by how the system is built. A user manages notifications, not webhook config. Describe what something is or does in plain terms rather than selling it. Being specific and legible to new users is always better than being clever.

Use active voice as default. A CTA says exactly what happens when it is used: "Save changes," not "Submit." An action keeps the same name through the whole flow, so the button that says "Publish" produces a toast that says "Published." The vocabulary of an interface is the signposting for someone navigating the product. Cohesion and consistency are how people learn their way around.

Treat failure and emptiness as moments for direction, not mood. Explain what went wrong and how to fix it, in the interface's voice rather than a person's. Errors don't apologize, and they are never vague about what happened. An empty screen is an invitation to act.

Keep the tone conversational: plain verbs, sentence case, no filler, with tone matched to the brand and the audience. Let each written element do exactly one job.
