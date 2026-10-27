# 安裝, 更新與換電腦

保存可攜的指示、角色、Skills 與工具設定, 在目標電腦逐項準備、載入與驗證, 個人路徑、登入資料與 credentials 留在該環境

## 先選管理項目與入口

| 項目 | 要處理的內容 | 操作方式 |
|---|---|---|
| 指示與角色 | Global、專案、subagent profile 與帳戶指示 | 比對來源、合併差異、核對載入 |
| Skills | 選定的工作流程與本機副本 | 核對名稱、版本與內容, 同步單項 |
| Plugins | 套件、啟用狀態與帳戶連接 | 依用戶端支援的管理介面處理 |
| MCP / CLI | 工具的相依、執行檔與註冊 | 依實際版本與授權逐項安裝或更新 |

先確認目標平台、用戶端與命令位置, 使用該版本支援的說明或管理介面查看參數, 安裝相依依選定項目處理

## 1. 取得教學與專案來源

在自己選擇的工作目錄取得 Playbook:

```text
git clone https://github.com/gaze9999/codex-playbook.git
```

直接閱讀 [開發流程](workflow.md) 與 [提示詞範例](prompts.md), 專案規格、指示與工具各依所屬來源取得, 已有 repository 時先檢查 remote、branch、status 與遠端更新

本 Playbook 的根目錄 AGENTS.md 是公開的專案指示教學範例, 私人設定另留在自己的設定來源, 換電腦維護時依 [指示管理](governance.md) 準備本機規則, research.md 隨 repository 保留作為教學參考

公開工具可使用 [Codex Toolkit 市集或獨立 Python](marketplace.md), 個人環境選項另保存在自己的私人設定來源, 不需要取得作者的私人 repository

### 用私人 workspace 管理相關儲存庫

需要共同開發、共用介面或跨專案協調時, 用私人父 repo 保存管理規範、子專案索引、角色來源與已審查的 submodule 指標, 各子 repo 保留自己的程式、歷史、版本與發布責任, 彼此沒有共同工作需求時可維持獨立 repo

| 層級 | 保存內容與責任 |
|---|---|
| Global | 跨專案偏好、授權與交付原則 |
| 私人 workspace | 需求分配、owner、相依、共用引用與整合驗收 |
| 子 repo | 自身架構、介面、實作、驗證與公開邊界 |
| 角色 / 條件式參考 | 必要的工作差異與方法, 可用角色不自動授權派工 |

共用 UI 可在需要的私人 workspace 各保留一份 checkout, 正式來源由同一儲存庫維護, 每份 checkout 的 branch、dirty 內容、父層 gitlink 與應用載入的版本/hash 各自核對, 不因資料夾同名就推定已同步或使用最新版本

公開子 repo 的私人工作規範放在私人父層, 本機入口只引用適用來源並精確排除版控, 子 repo 自有的已追蹤規範維持其 ownership, 明確散布的中性 Skill / Plugin 與範本另依公開來源維護. 私人父 repo 不改變公開子 repo 的可見性, 公開 diff、歷史及產物仍需核對, 私人 UI 來源與設定不隨公開工具散布

Codex 專案可將 workspace 設為主要來源以協調子專案, 主要資料夾決定預設 Git 與指示/config 探索, 次要資料夾要明確讀取及配對, worktree / Handoff 不自動隔離所有子 repo, 見 [Projects](https://learn.chatgpt.com/docs/projects) 與 [Worktrees](https://learn.chatgpt.com/docs/environments/git-worktrees). 修改時先確認實際子 repo, 提交並核對子 repo 遠端後再更新父層指標, 還原使用已審查基準, 不讓父子索引追逐彼此最新 SHA

### 整理分支與選定公開內容

先核對 main、工作分支、stash、未提交內容、其他 worktree 與即時遠端, 查明父 repo、Cloud 配方及部署 workflow 的引用, 保存並驗證完整私人 Git bundle 後, 再比較仍缺的有用內容與目前正式來源

| 比較結果 | 處理方式 |
|---|---|
| 已由新版涵蓋或取代 | 保留備份, 未使用且無有效引用時才移除舊分支/stash |
| 仍有需要的差異 | 併入目前 owner 後驗證, 保留其他修改與原始證據 |
| 檔案樹相同但歷史不同 | 核對身分/私人路徑清理範圍, 不按提交日期或遠端位置選擇 |
| 舊歷史會帶回已移除資料 | 只移植允許的差異到清理後主線, 不直接合併整段舊歷史 |
| main 推送會部署 | 完成該專案發布驗收並取得部署授權, 之前保留工作分支 |

私人 repo 可保留自身工作規範與角色, 選定公開交付則核對檔案/欄位允許清單、產物與實際公開歷史, 私人來源可讀不等於可公開, 完整方法見 [公開與私人交付](https://github.com/gaze9999/codex-toolkit/blob/main/skills/agent-governance/references/public-private-delivery.md#consolidate-branches-and-stashes-when-requested)

## 2. 準備 Global 指示與角色設定

查到需要使用者確認的身分、帳戶或設定值時, 先列確切結果、來源與預計用途, 等明確確認後才套用, 已確認且仍在原範圍內的選擇沿用

確認目標用戶端使用的 Global 指示與角色設定位置, 先備份現有內容, 比對可攜來源後合併需要的規則, 保留 model、provider、MCP、permissions 與登入資料

Profile 是一組執行設定, 啟用方式依用戶端的實際版本處理, 專案指示依模組責任與驗收改寫, 角色檔案已保存後仍需核對載入與權限, 詳見 [新專案的 agent 規劃](governance.md#新專案的-agent-規劃)

## 3. 安裝需要的 Skills

依目前任務選一項 Skill, 先讀啟用條件、預期交付、版本與相依, 再核對可攜來源和已安裝副本的差異

保存本機自訂內容, 確認同步範圍與取代方式後, 使用目標用戶端支援的安裝入口, .system、第三方 Plugin 與自行維護的 Skills 各由所屬來源管理

以相對路徑與內容 hash 比對來源和安裝副本, 鏡像一致證明檔案同步, 重新載入後再確認 Skill 的使用時機與實際產出, 工作流程範例見 [工具化規劃](toolkit-roadmap.md#可搭配的工作流程)

以 Codex Toolkit 的版本管理為例, 個別 Skill 採 SemVer, 與整包 release Tag 分開, 未修改的 Skill 保留版本, metadata 保存 `1.2.3`, 顯示名稱可標為 `Name (v1.2.3)`, 發布 manifest 記錄每項 Skill 的實際版本

## 4. 依電腦用途選工具

| 工作 | 需要的能力 |
|---|---|
| 程式開發 | 程式碼搜尋、專案檢查、UI 驗證與除錯 |
| 遊戲開發 | 共用規則測試、數值平衡與模擬 |
| 設計 | 研究、原型與視覺化 |
| 文件 | 文件讀寫、試算表與校對 |
| 研究 | 搜尋、論文與資料整理 |
| 個人服務 | 生活資訊、學習與帳戶功能 |

先沿用目前可用的能力, 缺少時每次選一個工具及其必要相依, 各工具的版本、帳戶、額度與資料範圍分開核對, 選用方式見 [工具介面](toolkit-roadmap.md#按任務選工具介面)

## 5. 完成工具連接與驗證

| 步驟 | 要確認的結果 |
|---|---|
| 檢查相依 | 平台、runtime、瀏覽器或桌面 App 符合要求 |
| 安裝工具 | 選定套件或執行檔可啟動 |
| 設定連接 | MCP 註冊指向正確位置與允許的資料範圍 |
| 帳戶授權 | API key、OAuth 與方案額度符合使用需求 |
| 載入工具 | 目前用戶端能找到工具與其參數 |
| 實際呼叫 | 一次代表性操作能取得預期結果 |

CLI 可直接在終端機使用, MCP 讓 agent 透過工具介面操作, 託管服務通常另需帳戶授權, 依所需能力選擇

使用已有的 CLI 或 GUI 管理入口, 核對平台與該版本的安裝方式, 工具的 initialize 測試只證明協定握手, 畫面列出註冊也只證明設定存在, 實際工具、帳戶流程與可讀寫資料範圍各自驗證

公司電腦依允許的資料範圍選工具, credentials 使用環境的正式保存方式, 公司與私人帳戶分開設定

用完後關閉自己建立的臨時 MCP client 與 browser session, 成功, 失敗或取消都清理, 用戶端管理的連線依其生命週期結束, 保留其他正在使用的工作

例如 Codex Toolkit 的 Serena 安裝設定停用 dashboard 與 GUI log window, 啟動參數包含 `--enable-web-dashboard false --enable-gui-log-window false`, 避免 Windows 為每條連線建立系統匣圖示, 依實際安裝版本核對設定

## 6. 更新已安裝工具

核對目前版本、更新來源、相容性與本機自訂內容, 使用該工具支援的預覽或更新方式, 套用前確認範圍並保存必要備份

Desktop、CLI 與 Plugin 使用各自官方更新通道, 專案 Framework 與 library 依該專案相容版本更新, 相依集中在所屬環境, 沿用 package manager 與 lockfile, 更新後重新載入並執行代表操作

Windows 更新 CLI 後確認命令位置與版本, 調整 PATH 前先備份並保留其他路徑, 重新開啟終端機或 App 以讀取新的環境

## 7. 套用介面中的設定

共用 Git 提示詞、記憶偏好與分支設定依目標介面提供的欄位套用, 產生設定片段時先核對相容性, 備份後再合併, 保留 model、provider、MCP、permissions 與其他設定

### 選用原生入口與私人設定來源

Plugin 的安裝、啟用與更新使用 Codex 支援的原生入口, 公開來源與操作見 [Toolkit 市集](marketplace.md), MCP 相依與註冊依 [Toolkit CLI](https://github.com/gaze9999/codex-toolkit/blob/main/docs/setup/cli.md) 逐項處理

自己的 Global、角色與 Desktop Git 提示詞保存在私人設定來源, 套用前產生差異或設定片段, 確認範圍後備份並合併, 保留其他設定與本機自訂內容, 還原方式見 [Toolkit Profile 指引](https://github.com/gaze9999/codex-toolkit/blob/main/docs/restore.md)

ChatGPT 帳戶指示、Project、雲端記憶與 Work 寫作風格在各自介面設定, 範例及位置見 [web-settings.md](web-settings.md)

套用後讀回內容, 在目標環境的新對話確認, 文件或片段已準備、設定已保存與實際生效分別回報, 記憶內容與私人權限規則留在個人環境

## 工作規範與 Plugin 的日常更新

先預覽選定來源與已安裝項目的差異, 再套用已授權範圍, 保存備份、來源版本及相對路徑 hash. Plugin 更新使用用戶端支援的原生入口, 保留其他套件、啟用狀態與帳戶, 不直接改 client 管理的快取

本機工作樹快照可用來試行尚未提交的修改, 需明確標示來源 HEAD 與未提交內容. 正式發布另依乾淨已提交來源及發布驗收, 本機同步不代表其他電腦已更新

先核對市集來源類型. GitHub 安裝的 Plugin 在來源發布後使用原生市集 / Plugin 入口更新, 保留 Git 來源. 已註冊的本機市集才使用限定工作樹快照同步, 不為立即套用未發布內容自動切換來源, 詳細操作見 [Toolkit Plugin 更新](https://github.com/gaze9999/codex-toolkit/blob/main/docs/plugins.md#已安裝-plugin-更新)

驗證工具記錄實際使用的 interpreter、版本與必要相依, 既有相容環境可重用, 工具或 bundled runtime 更新後先確認能力是否仍存在. 來源正確、同步一致、安裝成功與新對話載入分別核對

### 確認目前對話是否已載入

| 核對項目 | 可以支持的結論 |
|---|---|
| 安裝檔案與來源的版本、相對路徑及 hash 一致 | 本機副本同步完成 |
| 目前對話收到最新 AGENTS.md 的辨識文字 | 該段規範已進入目前對話 |
| Skill 名稱與來源出現在目前可用清單 | 該 Skill 已被探索, 完整內容仍按需讀取 |
| 讀取選定 Skill 的 SKILL.md 與必要 references | 本次已取得相應版本的工作流程 |
| 實際使用更新後的 Desktop Git 指示產生文字 | 該次操作已取得指示, 另核對是否符合新內容 |

Skills 採按需載入, 清單存在、安裝檔可讀與本次已使用完整流程分開回報, 見 [官方 Skills 說明](https://learn.chatgpt.com/docs/build-skills). 用戶端未提供目前對話的載入狀態或重新探索入口時, 保留未驗證項目, 重新載入後再在目標對話核對, 另一個 CLI 程序的清單不能證明已開啟對話的狀態

### 遷移專案資料夾與清理舊入口

先核對正在使用的專案來源、可寫 roots、checkout/worktree 與檔案引用, 用目前版本支援的專案設定或 API 更新, 讀回保存內容, 再確認執行中的 App 採用與相關入口操作, 另一個 CLI / App Server 的結果只證明該程序狀態

歷史路徑先依來源、actor、封存/執行狀態及目前引用分辨用途, 系統審查、subagent 歷史與備份保留原始證據, 不因出現舊路徑就重啟工作或改權限. 查核使用不恢復工作的讀取入口, [App Server 的 thread/read](https://learn.chatgpt.com/docs/app-server#read-a-stored-thread-without-resuming) 與 resume 行為不同, 參數依目前 client/schema 核對

Windows 磁碟路徑、延伸前綴與 URI/cache key 依欄位規格比對, 只改選定欄位, 保存 hash 與備份, 套用前重查, 映射碰撞或同時修改就停止. 有效引用及使用端驗證通過後, 核對連結 ownership、類型與確切 target, 只移除相容連結本身, 保留實體資料、其他 worktree 與歷史, 再檢查正式入口

## 8. 換機後開始工作

在目標專案確認適用指示、branch、HEAD、未提交變更與必要本機檔案, 再核對 model、工具、格式化與測試方式

平行工作時安排共用服務、ports 與測試資料, 使用新 worktree 時重新核對這些項目

保存來源版本、比對結果、實際呼叫與待處理事項, 個人路徑放在私人紀錄

## 9. 核對 Git 身分與公開內容

個人與公司工作可用各 repository 的 Git 設定或 conditional include 分開署名, GitHub noreply email 從自己的帳號設定取得

提交前檢查待提交內容與作者資料, 本機設定、logs、備份與 credentials 由 .gitignore 排除, 已受追蹤的檔案另外取消追蹤

要修改既有歷史時另確認範圍, 先備份並核對協作者與遠端 refs, 再依授權處理
