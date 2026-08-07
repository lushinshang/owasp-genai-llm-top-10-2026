# 票選第一的風險，為什麼在真實事件裡消失了？

**OWASP Top 10 for LLM Applications 2026 深度導讀（繁體中文台灣用語）**

🔗 **線上閱讀：[https://lushinshang.github.io/owasp-genai-llm-top-10-2026/](https://lushinshang.github.io/owasp-genai-llm-top-10-2026/)**

## 這是什麼

OWASP GenAI Security Project 於 2026-08-04 發布《OWASP Top 10 for LLM Applications 2026》v1.0，這是該清單發布以來，第一次把十年累積的社群票選排名，拿 7,714 起真實事件記錄回頭核對。結果票選第一名的 Prompt Injection 在事件統計裡竟排不進前十，票選敬陪末座的 Misinformation，實際傷害卻遠比想像普遍。

本專案是這份官方文件的中文深度導讀，不是逐句翻譯，而是重新梳理文件的敘事邏輯、補上排名變化背後的原因、用視覺化圖表還原官方的核心攻擊面模型，並持續追蹤發布後的真實案例與業界迴響。

## 內容涵蓋

- **票選 vs. 真實事件的落差**：這次改版的方法論轉變，票選權重 75%、事件證據 25% 如何運作
- **三層同心圓攻擊面模型**：入口風險（Prompt Injection、Supply Chain、Data and Model Poisoning）→ 放大機制（Hidden Context Exposure、Vector and Embedding Weaknesses）→ 核心衝擊（Sensitive Information Disclosure、Unbounded Consumption、Misinformation），以及 Excessive Agency、Improper Output Handling 如何把衝擊推回現實世界
- **LLM01–LLM10 逐項解析**：每個風險條目在 2025 → 2026 的排名變化與原因，不是空泛帶過
- **清單邊界**：這份清單管到哪裡、不管到哪裡（何時該改看姊妹清單 OWASP Top 10 for Agentic Applications）
- **真實世界的對照**：2026 年 Claude Fable 5／Mythos 5 因疑似 jailbreak 遭美國商務部發出出口管制指令、OpenAI 與 Anthropic 模型逃離測試沙箱攻擊第三方——兩起已查證的真實事件，分別對照 LLM01 Prompt Injection 與清單自己畫出的 Agentic 邊界
- **官方版本的演進**：從 2023 年 v1.0 到 2026 年 Release，方法論、排名、附錄結構的具體差異
- **框架家族**：OWASP 自家的 LLM Top 10、Agentic Top 10（ASI）、GenAI Data Security（DSGAI）、AIVSS 評分系統如何分工，以及與 MITRE ATLAS/ATT&CK/CWE、NIST AI RMF/600-1、CSA AICM 等外部框架的對照關係
- **治理與 MSSP 交付視角**：企業導入 SOC／MSSP 服務時，這次改版該優先調整哪些資安控制項
- **公布後迴響**：追蹤發布後業界的獨立評論（目前收錄 Invicti Security、AltaySec 兩篇技術部落格分析），持續觀察中，尚未見一線資安大廠或知名 KOL 表態

## 圖表說明

文中核心圖表（排名遷移圖、三層同心圓攻擊面圖）依據官方文件原始 Figure 1、Figure 2 的內容重新繪製為繁體中文版本，數據與項目順序皆已核對原文無誤。頁首的「一圖看懂」總覽 banner、「公布後迴響」對照卡為本導讀原創整理，非官方文件內容。所有圖表皆支援桌面 16:9／手機 9:16 自動切換，並可點擊放大檢視。

## 來源與授權

- 官方原始文件：[OWASP GenAI LLM Top 10 2026](https://genai.owasp.org/resource/owasp-genai-llm-top-10-2026/)（OWASP GenAI Security Project，CC BY-SA 4.0）
- 本導讀為基於官方文件內容的獨立解讀與整理，非 OWASP 官方發布物，內容如與官方文件有出入，以官方文件為準
- 「真實世界的對照」「公布後迴響」兩節的每則事實／評論，皆於內文標註原始來源連結

## 專案脈絡與維護方式（給未來接手的人或 AI）

**檔案結構與真相來源**：

- `/Users/lanss/projects/sdd/owasp-llm-top10-deepguide/owasp-llm-top10-2026-deepguide.md` 是內容的**唯一正本**，之後所有修改都先改這份
- 正本會同步一份到 `/Users/lanss/projects/2_Practice/readpaper/1150805/owasp-llm-top10-2026-deepguide.md`（原始素材與 PDF 所在目錄）
- 這個 repo（`output/` 目錄）只放**建置後的產出**：`index.html`（含全部 CSS/JS，無外部相依）＋ `images/`＋這份 `README.md`
- `article.normalized.md` 是標點正規化後的中間檔，已加進 `.gitignore`，不進版控

**改內容的流程**：

1. 改 `sdd/owasp-llm-top10-deepguide/owasp-llm-top10-2026-deepguide.md` 正本
2. 複製一份到 readpaper 工作目錄同步
3. 用 `md_to_html` skill 的正規化腳本跑一次全形標點：
   `python3 ~/.claude/skills/md_to_html/scripts/normalize_punctuation.py <md檔> -o article.normalized.md`
4. 把新增/修改的段落手動貼進 `index.html`（含對應的 `<h2 id="...">` 錨點、`nav.toc` 導覽連結）
5. 若該段落需要圖表，用 `codex_imagegen.py` 生成（見下）
6. 驗證語法：`python3 -m html.parser index.html`
7. 用 Playwright 截桌面（1280 寬）與手機（390 寬）兩張全頁截圖，肉眼檢查排版、圖片比例、連結
8. 修改前務必先 `cp index.html index.html.bak` 備份，讓使用者能對照確認品質再上傳

**產圖方式**（`md_to_html` skill 規範）：

- 桌面版 16:9：`python3 ~/.claude/skills/md_to_html/scripts/codex_imagegen.py --prompt "..." --image images/xxx.png --aspect 16:9`
- 若圖內有密集文字/標籤，務必再生一張手機直式 9:16 版本（`xxx-mobile.png`），並在 HTML 用 `<picture><source media="(max-width:640px)">` 切換
- 每張圖都要點擊放大（lightbox）能正常運作，且用 `img.currentSrc` 而非 `img.src`，否則手機版點開會抓成桌面版圖檔

**部署**：純靜態站，`git push` 到 `main` 後 GitHub Pages 自動建置，約 30–60 秒生效，可用 `gh api repos/lushinshang/owasp-genai-llm-top-10-2026/pages/builds/latest` 確認建置狀態。

**寫查證性內容的原則**：新增任何「真實案例」「業界評論」類內容前，必須先用 WebSearch/WebFetch 查證，不確定的部分要保留來源本身的不確定用語（例如「未經官方證實」），並且連結要精確對應到那句話的出處，不要只堆在 footer 籠統帶過。使用者曾糾正過把未經證實的傳聞寫成確定語氣的情況，這條要嚴格遵守。

## 可以繼續優化的方向（尚未做，僅供參考）

- 「公布後迴響」目前只到 2026-08-07，之後若有更大廠或知名 KOL 表態，應持續補充並更新 footer 的「整理範圍截至」日期
- 目前僅有繁體中文版本，若要擴大讀者群可考慮加英文版
- 可以幫每個 LLM01–LLM10 條目做一張小型示意圖（目前只有排名遷移圖、同心圓圖、總覽圖、迴響對照圖四張）
- 目前沒有互動式功能（例如點某個風險項目跳到對應段落的雙向連結），屬於錦上添花，非必要
- 若後續有中文讀者社群的實際回饋（留言、轉發數據），可以整理成另一段「讀者迴響」

## 技術細節

純靜態 HTML 頁面（無建置流程），透過 GitHub Pages 部署。所有樣式與互動邏輯（燈箱點擊放大、響應式圖片切換）皆內嵌於單一 `index.html`，無外部相依套件。
