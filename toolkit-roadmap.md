# Skill 與通用工具怎麼規劃

先找目前缺少的工作能力, 再決定補 Skill、整合現有工具或抽出共用程式, 依本頁選擇工作流程與介面, 相依準備及實際呼叫驗證見 [安裝與換機](portability.md)

## 先決定放哪裡

| 工作特性 | 適合位置 |
|---|---|
| 需要解讀需求, 判斷來源與取捨 | Skill |
| 輸入輸出明確, 可測試且能獨立使用 | 所屬工具的 CLI 或共用程式 |
| Codex 工具註冊, Skill 安裝與連接 | 所屬用戶端與設定來源 |
| 教學, 採用理由與範例 | codex-playbook |
| 個人興趣, 學習紀錄與排程 | 私人筆記與已授權的排程 |

例如, 決定文件如何改寫屬於 Skill, 檢查標題層級與檔案 hash 屬於工具, 讓 Codex 能呼叫這個工具屬於整合

獨立產品維持自己的 repository, 共用程式由一個來源維護, 各使用者依版本引用

## 按任務選工具介面

先確認要取得的結果與證據, 沿用目前可用且相容的入口, CLI 提供可重現操作, Skill 說明使用條件與驗收, MCP / connector 依 client 與 server 的能力提供串接, Plugin 的管理依目標用戶端處理

| 需求 | 選擇與核對方式 |
|---|---|
| 檔案搜尋、Git、批次處理與專案檢查 | 優先既有 CLI, 核對解析到的執行檔、版本、參數與副作用 |
| 帳戶服務或 client 原生能力 | 沿用已認證且可呼叫的 MCP / connector, 核對 live schema、帳戶與資料範圍 |
| Browser UI 重現與驗收 | 已知流程可用具名隔離的 CLI session, 需要特定頁面操作或診斷證據時選符合需求的 browser tools |
| 文件來源、Markdown 與證據比對 | 明確路徑的單次處理可用 CLI, 反覆受限查詢可用具備 roots / hash 檢查的 MCP |
| 本機文字校對 | 使用相符語言的 CLI 或已載入工具, 核對自動寫檔與回傳建議的差異 |
| 遊戲規則與數值模擬 | 使用專案共用規則與既有測試工具, 再依問題補計算、試算表或繪圖能力 |

能回傳 JSON、登入帳戶或保留狀態的 CLI 也可能足以完成工作, 兩種介面都符合需求時, 比較完整任務的完成率、重現與恢復方式、用量、時間及維護成本, 介面選擇保留同一套授權與外傳邊界

候選清單、安裝完成、設定已註冊、目前 session 已載入、帳戶已授權與實際呼叫成功分開核對, 缺少能力只阻擋相依部分, 安裝或擴大 roots 依該動作的授權處理

自訂 Skill 與第三方 Plugin 分別沿用自己的管理來源, 核對 Plugin 的安裝、啟用狀態、帳戶連接與實際能力, Skill 鏡像同步只證明其檔案狀態

## 可搭配的工作流程

以下名稱是依工作能力分組的 Skill 範例, 使用前確認目前環境是否具備、啟用條件是否相符, 沒有對應 Skill 時仍可依本指南完成相關工作

| Skill | 使用時機 |
|---|---|
| agent-governance / task-routing | 規劃指示分層與角色 / 判斷當次工作分流與交接 |
| context-brief / task-guide / coding-prompt | 整理指定實作規格 / 維護功能導覽 / 產生單次 coding prompt |
| angular-development / angular-member-order | 依實際 Angular 版本處理元件、表單與串接 / 安全整理成員順序 |
| react-development / vue-development | 依實際 Framework、state 與 rendering 邊界開發及驗證 |
| system-design-analysis | 整理需求, 領域模型, 資料一致性與架構取捨 |
| research-learning-synthesis | 整合官方資料, 社群與論文, 保存反例與先備概念 |
| development-tool-setup | 檢查並設定一項選定工具的相依與連接 |
| multilingual-proofreading | 校對繁中, 英文與日文的用詞, 標點與語意 |
| ui-ux-design | 從代表流程改善介面, 文案, 響應式與鍵盤操作 |
| game-balance-simulation | 沿用實際遊戲規則比較策略、進度與隨機獎勵, 保留重播條件 |
| document-source-matching / validation-evidence-review | 核對文件來源 / 檢視既有驗證證據, 保留版本與涵蓋範圍 |
| network-filter-rules | 依目標解析器維護阻擋或 rewrite 規則, 檢查誤判 |

提示詞評估可擴充 ai-application-engineering 的參考流程, Coding 交接提示詞由 coding-prompt 處理

先閱讀與交付相符的 Skill 啟用條件, 實作、唯讀審查與只產生 prompt 各依原始授權交付, 例如 coding-prompt 產生 prompt 時不直接執行, doc-updater 依可核對的實作變更更新既有文件

Stable Diffusion / ComfyUI 沿用 comfyui-workflow, Unity 專案沿用 unity-development, 安全檢查使用適用的安全工作流程

遊戲數值流程見 [game-balance.md](game-balance.md), 引擎與場景維護留在各專案工作流程, 通用 Skill 與工具設定由所屬來源維護

有真實 ML 實驗專案後, 再補資料來源, 訓練與測試切分, seed, 環境, model 設定及指標比較

## 哪些部分適合工具化

| Skill / 群組 | 目前方向 | 實作前要確認 |
|---|---|---|
| document-source-matching | 沿用文件定位與來源比對工具 | 原始文件, 抽出版與缺漏情況 |
| environment-consistency-check | 沿用目錄與檔案比對工具 | 相對路徑, hash 與差異種類 |
| validation-evidence-review | 沿用驗證紀錄索引 | 結果對應的內容版本與環境 |
| document-production | 有既有工具時沿用 Markdown 結構檢查核心 | 其他格式的內容與渲染檢查 |
| context-brief | 比較既有文字抽取與 OCR 工具 | 格式, metadata, 相依與失敗處理 |
| doc-updater | 評估抽出 Git 變更分類與安全寫入 | 整檔或章節更新, 備份與衝突處理 |
| task-guide | 有重複案例時抽出資料驗證與歷史追加 | 文件格式與可共用範圍 |
| angular-member-order | Skill 判斷成員順序 | initializer, decorator 與非同步時序 |
| comfyui-workflow | 評估流程與環境清單比對 | 實際 graph 格式與版本案例 |
| ai-application-engineering | 整理評估紀錄與 metrics | 既有評估方法與比較條件 |
| jev-evaluation | 共用 client, 用戶端串接依其介面管理 | 資料邊界與結果語意 |
| license-maintainer | 掃描授權 metadata 與 SPDX 候選 | 來源, 權利歸屬與實際授權 |
| network-filter-rules | 使用目標引擎的 validator | 該平台的規則語意 |
| agent-governance / task-routing / coding-prompt | 保留需求與分工判斷流程 | 目標, 責任與授權 |
| readme-maintainer / editorial-illustration | 保留來源判讀與創作流程 | 交付要求與實際材料 |
| unity-development / angular-development / react-development / vue-development | 使用專案原生檢查 | 引擎與 Framework 的工具鏈 |
| game-balance-simulation | 沿用共用規則執行 headless 實驗 | 時間、隨機輸入、策略與可重播的失敗案例 |

## 什麼時候拆分或合併 Skill

比較使用時機與交付物, 同一入口的詳細情境可移到參考文件, 有相同目的且反覆一起使用的流程再評估合併

| 群組 | 各自保留的責任 |
|---|---|
| agent-governance / task-routing | 維護規則與角色 / 安排當次工作 |
| readme-maintainer / doc-updater / document-production | 重整 README / 同步變更 / 製作文件 |
| context-brief / task-guide / coding-prompt | 規格摘要 / 功能工作指引 / 單次交接 |
| angular-development / system-design-analysis / research-learning-synthesis | Framework 實作與按需架構 / 系統取捨 / 證據整理 |
| document-source-matching / environment-consistency-check / validation-evidence-review | 文件來源 / 內容比對 / 驗證證據 |

Skills 的發布組合包保留獨立目錄, 每項清單、metadata 與版本由其維護來源管理

## 抽出共用程式的步驟

1. 找一個有重複使用需求的功能, 保存代表輸入與預期輸出
2. 核對參數, exit code, encoding 與不完整輸入的處理
3. 確認 dry-run, 寫入, 備份, 原子更新與 hash 比對行為
4. 將實作放在一個版本化核心, 各入口引用同一份邏輯
5. 用原有案例比較結果, 再更新相依的整合程式

原子更新是先完成新內容再一次替換目標, 用來避免只寫入一半的檔案, 需要獨立副本時從核心產生並記錄版本與來源 hash

## 下一步怎麼排

有共用核心時先核對支援格式與內容版本, 後續優先評估真實重複案例, 例如文件安全寫入, Git 變更分類與 OCR 整合

先確認輸入輸出相容與維護收益, 每次遷移一個功能並核對原有行為, 原始碼與實作狀態以各工具來源為準
