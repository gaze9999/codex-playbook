# Skill 與通用工具怎麼規劃

先找目前缺少的工作能力, 再決定補 Skill, 整合現有工具或抽出共用程式, 可用清單見 [codex-setup](https://github.com/gaze9999/codex-setup#skill-catalog)

## 先決定放哪裡

| 工作特性 | 適合位置 |
|---|---|
| 需要解讀需求, 判斷來源與取捨 | Skill |
| 輸入輸出明確, 可測試且能獨立使用 | my-py-tools 的 CLI 或共用程式 |
| Codex 工具註冊, Skill 安裝與連接 | codex-setup |
| 教學, 採用理由與範例 | codex-playbook |
| 個人興趣, 學習紀錄與排程 | 私人筆記與已授權的排程 |

例如, 決定文件如何改寫屬於 Skill, 檢查標題層級與檔案 hash 屬於工具, 讓 Codex 能呼叫這個工具屬於整合

獨立產品維持自己的 repository, 共用程式由一個來源維護, 各使用者依版本引用

## 已有的工作流程

| Skill | 使用時機 |
|---|---|
| angular-architecture | 依專案版本分析 DI, 狀態生命週期, 路由與模組邊界 |
| system-design-analysis | 整理需求, 領域模型, 資料一致性與架構取捨 |
| research-learning-synthesis | 整合官方資料, 社群與論文, 保存反例與先備概念 |
| development-tool-setup | 檢查並設定一項選定工具的相依與連接 |
| multilingual-proofreading | 校對繁中, 英文與日文的用詞, 標點與語意 |
| ui-ux-design | 從代表流程改善介面, 文案, 響應式與鍵盤操作 |

提示詞評估可擴充 ai-application-engineering 的參考流程, Coding 交接提示詞由 coding-prompt 處理

Stable Diffusion / ComfyUI 沿用 comfyui-workflow, Unity 專案沿用 unity-development, 安全檢查使用適用的安全工作流程

有真實 ML 實驗專案後, 再補資料來源, 訓練與測試切分, seed, 環境, model 設定及指標比較

## 哪些部分適合工具化

| Skill / 群組 | 目前方向 | 實作前要確認 |
|---|---|---|
| document-source-matching | 沿用文件定位與來源比對工具 | 原始文件, 抽出版與缺漏情況 |
| environment-consistency-check | 沿用目錄與檔案比對工具 | 相對路徑, hash 與差異種類 |
| validation-evidence-review | 沿用驗證紀錄索引 | 結果對應的內容版本與環境 |
| document-production | Markdown 結構檢查已有共用核心 | 其他格式的內容與渲染檢查 |
| context-brief | 比較既有文字抽取與 OCR 工具 | 格式, metadata, 相依與失敗處理 |
| doc-updater | 評估抽出 Git 變更分類與安全寫入 | 整檔或章節更新, 備份與衝突處理 |
| task-guide | 有重複案例時抽出資料驗證與歷史追加 | 文件格式與可共用範圍 |
| component-member-order | Skill 判斷成員順序 | initializer, decorator 與非同步時序 |
| comfyui-workflow | 評估流程與環境清單比對 | 實際 graph 格式與版本案例 |
| ai-application-engineering | 整理評估紀錄與 metrics | 既有評估方法與比較條件 |
| jev-evaluation | 共用 client, Codex 連接留在 setup | 資料邊界與結果語意 |
| license-maintainer | 掃描授權 metadata 與 SPDX 候選 | 來源, 權利歸屬與實際授權 |
| filter-rule-maintenance | 使用目標引擎的 validator | 該平台的規則語意 |
| agent-governance / task-routing / coding-prompt | 保留需求與分工判斷流程 | 目標, 責任與授權 |
| readme-maintainer / editorial-illustration | 保留來源判讀與創作流程 | 交付要求與實際材料 |
| unity-development / vue-development | 使用專案原生檢查 | 引擎與 Framework 的工具鏈 |

## 什麼時候拆分或合併 Skill

比較使用時機與交付物, 同一入口的詳細情境可移到參考文件, 有相同目的且反覆一起使用的流程再評估合併

| 群組 | 各自保留的責任 |
|---|---|
| agent-governance / task-routing | 維護規則與角色 / 安排當次工作 |
| readme-maintainer / doc-updater / document-production | 重整 README / 同步變更 / 製作文件 |
| context-brief / task-guide / coding-prompt | 規格摘要 / 功能工作指引 / 單次交接 |
| angular-architecture / system-design-analysis / research-learning-synthesis | Framework 架構 / 系統取捨 / 證據整理 |
| document-source-matching / environment-consistency-check / validation-evidence-review | 文件來源 / 內容比對 / 驗證證據 |

Skills 的發布組合包保留獨立目錄, 實際清單與 metadata 由 codex-setup 維護

## 抽出共用程式的步驟

1. 找一個有重複使用需求的功能, 保存代表輸入與預期輸出
2. 核對參數, exit code, encoding 與不完整輸入的處理
3. 確認 dry-run, 寫入, 備份, 原子更新與 hash 比對行為
4. 將實作放在一個版本化核心, 各入口引用同一份邏輯
5. 用原有案例比較結果, 再更新相依的整合程式

原子更新是先完成新內容再一次替換目標, 用來避免只寫入一半的檔案, 需要獨立副本時從核心產生並記錄版本與來源 hash

## 下一步怎麼排

Markdown 結構檢查已有共用核心與產生的獨立副本, 後續優先評估真實重複案例, 例如文件安全寫入, Git 變更分類與 OCR 整合

先確認輸入輸出相容與維護收益, 每次遷移一個功能並核對原有行為, 原始碼與實作狀態以各工具來源為準
