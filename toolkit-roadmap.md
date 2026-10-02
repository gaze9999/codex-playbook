# Skill 與 Python 工具的缺口評估

2026-10-02 依 codex-setup 的 20 個 managed Skills, my-py-tools 的 CLI / core 文件與相關 helper 原始碼檢視. 以下是候選與拆分建議, 不表示已實作, 搬移或完成行為等價驗證; 新版本應重新核對來源

## 先決定放哪裡

| 工作特性 | 適合位置 |
|---|---|
| 需要解讀目標, 取捨與來源證據 | Skill 的條件式流程, Main 保留最後判斷 |
| 確定性輸入輸出, 可測試且不依賴 Codex | my-py-tools 的 CLI / versioned core |
| Codex 工具註冊, Skill 安裝或 runtime adapter | codex-setup |
| 個人興趣, 學習程度, 排程與收藏處置 | 私人筆記 / dot |
| 教學, 採用理由, 可分享範例 | codex-playbook |

Skill 可以呼叫工具, 不必整份改寫成 Python; 工具輸出的候選或結構檢查也不能代替語意正確性與驗收. 獨立產品仍保留自己的 repo, 不因有 Python 就全部搬進 my-py-tools

## 新 Skill 候選

| 優先順序 | 候選 | 真正缺少的流程 | 先避免的重複 |
|---|---|---|---|
| 優先 | Angular 架構分析 | 依版本追蹤 DI / provider scope, state lifetime, Signals / RxJS, routing, rendering, 模組與 custom-element 邊界; 交付現況圖, 風險及最小變更方案 | component-member-order 只處理成員排序等局部工作; 不複製專案規格, 不固定 Angular 版本 |
| 優先 | 系統設計與分析 | 將需求, 領域模型, 非功能需求, 資料與一致性, 介面及部署限制整理成可驗證取捨 | 不套固定架構模板, 不把每個 coding task 變成架構 review |
| 優先 | 研究整理與學習缺口 | 整合原始資料, 社群與論文證據; 區分事實與推論, 保留反例, 先備概念及有價值旁支 | dot 管排程, Skill 管研究方法; 不再建立重複排程或無限制收藏庫 |
| 有實驗需求後 | ML 實驗工作流 | 保存 dataset split / provenance, seed, environment, training / inference 設定, metrics 與比較條件 | 不限 PyTorch, 不預先下載資料或模型; 有真實實驗 repo 再定具體流程 |

提示詞評估優先擴充 ai-application-engineering 的條件式 reference, 保留代表案例, failure cases, prompt / model 版本及成本比較; 純 coding prompt 繼續由 coding-prompt 處理

Stable Diffusion / ComfyUI 已有 comfyui-workflow; 遊戲開發已有 unity-development, 尚未確定引擎時不把 Unity 當預設. 紅隊已有 codex-security plugin, 不複製一套競爭的掃描流程. 網站操作先用已存在的 browser / computer-use 能力, 具體重複購物流程成熟後再建立有狀態與授權邊界的工具

## 現有 Skills 的工具化判斷

| Skill / 群組 | 建議 | 依據與限制 |
|---|---|---|
| document-source-matching | 沿用既有工具, 不新增 | 已使用 documents.locate_markdown_extracts / local_documents; hash 一致不等於抽取完整 |
| environment-consistency-check | 沿用既有工具, 不新增 | 已使用 maintenance.environment_consistency / workspace_inspection; 比對不授權同步 |
| validation-evidence-review | 沿用既有工具, 不新增 | 已使用 validation.validation_evidence_index; 索引成功不等於驗收通過 |
| document-production | 通用 validator 優先工具化候選 | 現有 validate_markdown / docx / pdf / apa7 scripts 可拆通用結構檢查與文件樣式規則; 視覺品質仍需閱讀 / 渲染驗證 |
| context-brief | 抽取 / OCR 先比較既有 core 再整合 | extract_source_text / ocr_fallback 與 my-py-tools 文件處理存在功能交集; 格式, OCR, fallback, metadata 與依賴差異未驗證前不可直接替換 |
| doc-updater | Git 變更分類可獨立, 安全寫入優先共用 core | scan_changed_files 不依賴 Codex; write_markdown_sync_target 與 guarded_markdown_update 的整檔 / 章節及預設寫入語意不同, 需先定相容介面 |
| task-guide | 視重複使用情況抽通用資料驗證 / 歷史追加 | create_task_guide / record_history 含特定文件 schema; 不把單一 task guide 格式強制成所有工具的標準 |
| component-member-order | Skill 保留語意判斷, 導覽沿用 Angular tools | 現有 generate_component_member_order_prompt 是 prompt helper; 不以 regex 自動搬動含 initializer / decorator / reactive 時序的成員 |
| comfyui-workflow | 將來可做 workflow / environment manifest 與差異報告 | 必須有實際 graph 格式與版本案例; 不重新做 runtime 已提供的圖驗證或把 JSON parse 當生成成功 |
| ai-application-engineering | 評估紀錄與 metrics 彙整可工具化 | 先沿專案已有 eval framework; model 品質判定和 provider 差異不宜硬編碼成通用分數 |
| jev-evaluation | client 可重用, Codex adapter 留 setup | 不因 CLI 可獨立執行就搬整套 MCP; telemetry 已有獨立監看產品, 不再複製 client 或用量統計 |
| license-maintainer | metadata / SPDX 候選掃描可工具化 | 法律授權與 ownership 仍需核對; 不讓檔名或字串比對自動決定 license |
| filter-rule-maintenance | 沿用目標引擎 validator | 平台語意不同, 不用自製 parser 宣稱相容或自行補允許規則 |
| agent-governance / task-routing / coding-prompt | 保留 Skill | 核心是需求, ownership, 授權與 context 取捨; 不適合以分數自動決定委派 |
| readme-maintainer / editorial-illustration | 保留 Skill | 核心是來源判讀或創作要求, 可使用既有格式檢查與影像工具 |
| unity-development / vue-development | 保留 Skill, 使用專案原生檢查 | 不另做取代引擎, compiler 或框架工具鏈的 Python validator |

## 建議實作次序

先補最常反覆發生的流程缺口, 再選一項確定性工具核心整合. 優先比較文件 validators 和已有 document core, 用代表性 fixtures 證明輸出與錯誤語意, 保留原 CLI 的相容入口後再切換 Skill

每次遷移只保留一個核心實作; 核對參數, exit codes, encoding, 不完整輸入, dry-run / write 預設, 原子寫入, backup 與 hash 行為. 不依賴另一個 working tree 的路徑, 以版本化套件使用核心. 新增工具不自動授權安裝依賴, 執行遠端服務或修改使用者檔案

沒有真實重複案例, 可測的輸入輸出或明確維護收益時先不建工具; 此清單是可修訂候選, 不作每輪必讀 checklist
