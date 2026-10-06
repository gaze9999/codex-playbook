# 安裝, 更新與換電腦

codex-setup 保存可攜來源, 本機 Codex 目錄保存安裝副本, 長期修改先回來源整理, 再同步到需要的電腦

這裡提供操作順序, CLI、GUI 與完整選項見 [codex-setup 文件索引](https://github.com/gaze9999/codex-setup/blob/main/docs/README.md)

## 先選管理項目與入口

| 類別 | 要處理的內容 | 操作方式 |
|---|---|---|
| agents | Global、subagent profile、Desktop 與帳戶指示來源 | 比對來源、安裝指定檔案、產生設定片段 |
| skills | 自訂 Skill 與本機鏡像 | 選定名稱、預覽差異、同步單項 |
| plugins | 已設定的 Plugin 與啟用狀態 | setup 檢視, Codex 官方介面安裝及連接帳戶 |
| mcp | 選定工具的相依、套件與註冊 | 預覽後依授權逐項安裝或更新 |

以下 Windows 命令在 codex-setup 根目錄執行, macOS / Linux 將 `.\launch-cli.cmd` 換成 `sh launch-cli.sh`, 已安裝 setup wheel 時使用 `codex-setup`, 每個動作可先查看 `--help`

```text
.\launch-cli.cmd --list
.\launch-cli.cmd agents --list
.\launch-cli.cmd skills --list
.\launch-cli.cmd plugins --list
.\launch-cli.cmd mcp --list
```

CLI 操作需要相容的 Python, 來源與指定方式見 [CLI 說明](https://github.com/gaze9999/codex-setup/blob/main/docs/setup/cli.md), 相依依選定項目檢查, 安裝缺項依該次授權處理

## 1. 取得來源

在自己選擇的工作目錄執行:

```text
git clone https://github.com/gaze9999/codex-playbook.git
git clone https://github.com/gaze9999/codex-setup.git
```

Playbook 直接閱讀, 可執行的指示與 Skills 從 codex-setup 安裝, 已有 repository 時先檢查 remote, branch, status 與遠端更新

本 Playbook 的根目錄 AGENTS.md 留在本機並由 .gitignore 忽略, 換電腦維護時依 [指示管理](governance.md) 準備本機規則, research.md 隨 repository 保留作為教學參考

## 2. 安裝 Global 指示與角色設定

第一與第三個命令做比對, 中間命令安裝:

```text
.\launch-cli.cmd agents global
.\launch-cli.cmd agents global --install
.\launch-cli.cmd agents global
```

安裝器使用 CODEX_HOME 或個人目錄下的 .codex, 也可用 --codex-home 指定位置, 管理 Global 指示與 subagent profile

既有檔案不同時先合併差異, 確定要取代才使用 `--install --replace`, 安裝器會先備份, 細節見 [治理設定](https://github.com/gaze9999/codex-setup/blob/main/docs/agents.md)

Profile 是一組執行設定, 安裝後依 [agents 說明](https://github.com/gaze9999/codex-setup/blob/main/docs/agents.md) 啟用, 修改本機設定時保留既有 MCP、permissions 與登入資料, project starter 需依實際專案改寫, 範本不代表角色已啟用

## 3. 安裝需要的 Skills

從 [Skill 清單](https://github.com/gaze9999/codex-setup/blob/main/docs/skills.md) 依目前需求選一項, 每個 Skill 獨立保存版本, 以 `agent-governance` 為例:

```text
.\launch-cli.cmd skills agent-governance
.\launch-cli.cmd skills agent-governance --apply
```

第一個命令預覽, 第二個在確認後同步, 將名稱換成所需 Skill, 來源不同或本機有自訂內容時先保存並處理差異, `--yes` 只用於該單項操作已獲授權的自動執行

需要可攜來源時, 使用 repository 的獨立 Skill 目錄或 release 的 all-skills 組合包, 解壓後選取需要的項目, 用戶端要求單項 ZIP 時依 [Skills 安裝說明](https://github.com/gaze9999/codex-setup/blob/main/docs/skills.md) 準備

只同步此來源管理的 Skills, 本機另有修改時先保存並合回來源, .system 與 plugin 由各自來源管理

檢查來源:

```text
.\launch-cli.cmd audit
```

要比對本機 Skills, 使用 `--installed-root` 指定安裝目錄, Audit 依相對路徑與內容 hash 比對, 詳細選項見 [audit 程式](https://github.com/gaze9999/codex-setup/blob/main/mcp/scripts/audit_skills.py)

鏡像一致證明檔案同步, 在目標用戶端重新載入後, 再確認 Skill 的使用時機與產出

## 4. 依電腦用途選工具

| 用途分類 | 適合的電腦與工作 |
|---|---|
| development | 程式開發, UI 驗證與除錯 |
| game | 遊戲開發、數值平衡與模擬 |
| design | 設計研究, 原型與視覺化 |
| office | 文件, 試算表與校對 |
| research | 搜尋, 論文與資料整理 |
| personal | 生活資訊, 學習與個人服務 |
| all | 查看全部候選工具 |

分類用來篩選選單, 每次選一個工具安裝, 各工具的相依與帳戶設定分開處理

Windows 使用 CMD:

```text
.\launch-cli.cmd mcp --profile development
```

macOS / Linux 使用 shell:

```text
sh launch-cli.sh mcp --profile development
```

上述命令在 codex-setup 根目錄執行, 可先使用 `mcp --list` 查看清單, 已安裝 setup wheel 時使用 `codex-setup mcp --profile development`, 可攜包依 [安裝包說明](https://github.com/gaze9999/codex-setup/blob/main/docs/setup/packages.md) 選相符平台

Python 相依依選定工具檢查, 入口支援的首次安裝詢問依 installer 提示處理, 詳見 [用途分類與更新](https://github.com/gaze9999/codex-setup/blob/main/docs/tools/workflows.md)

## 5. 完成工具連接與驗證

| 步驟 | 要確認的結果 |
|---|---|
| 檢查相依 | 平台, Python, Node, 瀏覽器或桌面 App 符合要求 |
| 安裝工具 | 選定套件或執行檔可啟動 |
| 設定連接 | MCP 註冊指向正確位置與允許的資料範圍 |
| 帳戶授權 | API key, OAuth 與方案額度符合使用需求 |
| 載入工具 | 目前用戶端能找到工具與其參數 |
| 實際呼叫 | 一次代表性操作能取得預期結果 |

Python server wheel 安裝 Python MCP, setup wheel 提供工具清單與安裝入口, Node 工具, 原生 App 與託管 MCP 保留各自接法

CLI 可直接在終端機使用, MCP 則讓 agent 透過工具介面操作, 託管服務通常另需帳戶授權, 依所需能力選擇

需要圖形介面時使用 `launch-gui.cmd` 或 `sh launch-gui.sh`, 從候選清單選定一項並預覽, 也可用 CLI 的 `--web` 開啟同一套管理介面, 來源編輯、Global 同步、Skill 鏡像與 Plugin 設定檢視依 [GUI 說明](https://github.com/gaze9999/codex-setup/blob/main/docs/setup/gui.md) 操作

管理器的 initialize 測試只證明協定握手, 畫面列出註冊也只證明設定存在, 實際工具、帳戶流程與可讀寫資料範圍各自驗證

完整接法:

- [核心 MCP](https://github.com/gaze9999/codex-setup/blob/main/docs/mcp.md)
- [開發工具](https://github.com/gaze9999/codex-setup/blob/main/docs/tools/development.md)
- [工具與服務清單](https://github.com/gaze9999/codex-setup/blob/main/docs/tools/catalog.md)
- [中英日校對](https://github.com/gaze9999/codex-setup/blob/main/docs/tools/proofreading.md)
- [UI / UX 與遊戲工具](https://github.com/gaze9999/codex-setup/blob/main/docs/tools/workflows.md)
- [Plugin 管理](https://github.com/gaze9999/codex-setup/blob/main/docs/plugins.md)

公司電腦依允許的資料範圍選工具, credentials 使用環境的正式保存方式, 公司與私人帳戶分開設定

## 6. 更新已安裝工具

`update` 查選定工具的更新, 預覽後加 `--apply` 套用, 已授權的單項自動執行可加 `--yes`

```text
.\launch-cli.cmd update --tool spartan
.\launch-cli.cmd update --tool spartan --apply
```

將 spartan 換成要更新的工具 ID, 實際可更新項目見 [更新說明](https://github.com/gaze9999/codex-setup/blob/main/docs/tools/workflows.md), setup wheel 在安裝它的獨立 venv 更新, venv 是該 Python 工具專用的環境

Desktop, CLI 與 plugin 使用各自官方更新通道, 專案 Framework 與 library 依該專案相容版本更新, 更新後重新載入並執行代表操作

Windows 更新 CLI 後確認命令位置與版本, 調整 PATH 前先備份並保留其他路徑, 重新開啟終端機或 App 以讀取新的環境

## 7. 套用介面中的設定

[Desktop 治理來源](https://github.com/gaze9999/codex-setup/blob/main/docs/agents.md) 集中在 `agents/`, 三個 Git 提示詞由 `git-instructions.toml` 維護, 記憶與分支偏好由 `desktop-preferences.toml` 維護

```text
.\launch-cli.cmd agents desktop
```

renderer 產生可合併片段, 先備份再合併到目標設定, 保留 model、provider、MCP、permissions 與其他設定, 單次產生片段只證明內容已準備

ChatGPT 帳戶指示, Project, 雲端記憶與 Work 寫作風格在各自介面設定, 範例及位置見 [web-settings.md](web-settings.md)

套用後讀回內容, 在目標環境的新對話確認, 記憶內容與私人權限規則留在個人環境

## 8. 換機後開始工作

在目標專案確認適用指示, branch, HEAD, 未提交變更與必要本機檔案, 再核對 model, 工具, 格式化與測試方式

平行工作時安排共用服務, ports 與測試資料, 使用新 worktree 時重新核對這些項目

保存來源版本, 比對結果, 實際呼叫與待處理事項, 個人路徑放在私人紀錄

## 9. 核對 Git 身分與公開內容

個人與公司工作可用各 repository 的 Git 設定或 conditional include 分開署名, GitHub noreply email 從自己的帳號設定取得

提交前檢查待提交內容與作者資料, 本機設定, logs, 備份與 credentials 由 .gitignore 排除, 已受追蹤的檔案另外取消追蹤

要修改既有歷史時另確認範圍, 先備份並核對協作者與遠端 refs, 再依授權處理
