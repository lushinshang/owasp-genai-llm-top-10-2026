# 票選第一的風險，為什麼在真實事件裡消失了？

**OWASP Top 10 for LLM Applications 2026 深度導讀（繁體中文台灣用語）**

🔗 **線上閱讀：[https://lushinshang.github.io/owasp-genai-llm-top-10-2026/](https://lushinshang.github.io/owasp-genai-llm-top-10-2026/)**

## 這是什麼

OWASP GenAI Security Project 於 2026-08-04 發布《OWASP Top 10 for LLM Applications 2026》v1.0，這是該清單發布以來，第一次把十年累積的社群票選排名，拿 7,714 起真實事件記錄回頭核對。結果票選第一名的 Prompt Injection 在事件統計裡竟排不進前十，票選敬陪末座的 Misinformation，實際傷害卻遠比想像普遍。

本專案是這份官方文件的中文深度導讀，不是逐句翻譯，而是重新梳理文件的敘事邏輯、補上排名變化背後的原因、並用視覺化圖表還原官方的核心攻擊面模型。

## 內容涵蓋

- **票選 vs. 真實事件的落差**：這次改版的方法論轉變，票選權重 75%、事件證據 25% 如何運作
- **三層同心圓攻擊面模型**：入口風險（Prompt Injection、Supply Chain、Data and Model Poisoning）→ 放大機制（Hidden Context Exposure、Vector and Embedding Weaknesses）→ 核心衝擊（Sensitive Information Disclosure、Unbounded Consumption、Misinformation），以及 Excessive Agency、Improper Output Handling 如何把衝擊推回現實世界
- **LLM01–LLM10 逐項解析**：每個風險條目在 2025 → 2026 的排名變化與原因，不是空泛帶過
- **清單邊界**：這份清單管到哪裡、不管到哪裡（何時該改看姊妹清單 OWASP Top 10 for Agentic Applications）
- **真實世界的對照**：2026 年 Claude Fable 5／Mythos 5 因疑似 jailbreak 遭美國商務部發出出口管制指令、OpenAI 與 Anthropic 模型逃離測試沙箱攻擊第三方——兩起已查證的真實事件，分別對照 LLM01 Prompt Injection 與清單自己畫出的 Agentic 邊界
- **官方版本的演進**：從 2023 年 v1.0 到 2026 年 Release，方法論、排名、附錄結構的具體差異
- **框架家族**：OWASP 自家的 LLM Top 10、Agentic Top 10（ASI）、GenAI Data Security（DSGAI）、AIVSS 評分系統如何分工，以及與 MITRE ATLAS/ATT&CK/CWE、NIST AI RMF/600-1、CSA AICM 等外部框架的對照關係
- **治理與 MSSP 交付視角**：企業導入 SOC／MSSP 服務時，這次改版該優先調整哪些資安控制項

## 圖表說明

文中兩張核心圖表（排名遷移圖、三層同心圓攻擊面圖）依據官方文件原始 Figure 1、Figure 2 的內容重新繪製為繁體中文版本，數據與項目順序皆已核對原文無誤。頁首的「一圖看懂」總覽 banner 為本導讀原創整理，非官方文件內容。所有圖表皆支援桌面 16:9／手機 9:16 自動切換，並可點擊放大檢視。

## 來源與授權

- 官方原始文件：[OWASP GenAI LLM Top 10 2026](https://genai.owasp.org/resource/owasp-genai-llm-top-10-2026/)（OWASP GenAI Security Project，CC BY-SA 4.0）
- 本導讀為基於官方文件內容的獨立解讀與整理，非 OWASP 官方發布物，內容如與官方文件有出入，以官方文件為準

## 技術細節

純靜態 HTML 頁面（無建置流程），透過 GitHub Pages 部署。所有樣式與互動邏輯（燈箱點擊放大、響應式圖片切換）皆內嵌於單一 `index.html`，無外部相依套件。
