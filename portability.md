# 安裝, 更新與換電腦

codex-setup 保存可攜來源, 本機 Codex 目錄保存安裝副本, 長期修改先回來源整理, 再同步到需要的電腦

這裡提供操作順序, 安裝器與完整選項見 [codex-setup](https://github.com/gaze9999/codex-setup)

## 1. 取得來源

在自己選擇的工作目錄執行:

```text
git clone https://github.com/gaze9999/codex-playbook.git
git clone https://github.com/gaze9999/codex-setup.git
```

Playbook 直接閱讀, 可執行的指示與 Skills 從 codex-setup 安裝, 已有 repository 時先檢查 remote, branch, status 與遠端更新

本 Playbook 的根目錄 AGENTS.md 留在本機並由 .gitignore 忽略, 換電腦維護時依 [指示管理](governance.md) 準備本機規則, research.md 隨 repository 保留作為教學參考

## 2. 安裝 Global 指示與角色設定

在 codex-setup 根目錄執行, 第一與第三個命令做比對, 中間命令安裝:

```text
python scripts/install_global_agents.py
python scripts/install_global_agents.py --install
python scripts/install_global_agents.py
```

安裝器使用 CODEX_HOME 或個人目錄下的 .codex, 也可用 --codex-home 指定位置, 管理 Global 指示與 subagent profile

既有檔案不同時先合併差異, 確定要取代才使用 --install --replace, 安裝器會先備份, 細節見 [安裝程式](https://github.com/gaze9999/codex-setup/blob/main/scripts/install_global_agents.py)

Profile 是一組執行設定, 安裝後依 [agents 說明](https://github.com/gaze9999/codex-setup/blob/main/agents/README.md) 啟用, 修改本機設定時保留既有 MCP, permissions 與登入資料

## 3. 安裝需要的 Skills

依 [安裝與同步說明](https://github.com/gaze9999/codex-setup#安裝與同步) 使用 repository 路徑或 release 組合包, 組合包內保留各 Skill 獨立目錄, 可選需要的項目

只同步此來源管理的 Skills, 本機另有修改時先保存並合回來源, .system 與 plugin 由各自來源管理

在 codex-setup 根目錄檢查來源:

```text
python scripts/audit_skills.py
```

要比對本機 Skills, 使用 --installed-root 指定安裝目錄, Audit 依相對路徑與內容 hash 比對, 詳細選項見 [audit 程式](https://github.com/gaze9999/codex-setup/blob/main/scripts/audit_skills.py)

## 4. 依電腦用途選工具

| 用途分類 | 適合的電腦與工作 |
|---|---|
| development | 程式開發, UI 驗證與除錯 |
| design | 設計研究, 原型與視覺化 |
| office | 文件, 試算表與校對 |
| research | 搜尋, 論文與資料整理 |
| personal | 生活資訊, 學習與個人服務 |
| all | 查看全部候選工具 |

分類用來篩選選單, 每次選一個工具安裝, 各工具的相依與帳戶設定分開處理

Windows 使用 CMD:

```text
install-mcp.cmd --profile development
```

macOS / Linux 使用 shell:

```text
sh install-mcp.sh --profile development
```

上述命令在取得安裝 bundle 並進入其目錄後執行, 輸入 --list 可先查看清單, 已安裝 setup wheel 時可使用 codex-mcp-setup --profile development

Python 相依依選定工具檢查, 入口支援的首次安裝詢問依 installer 提示處理, 詳見 [用途分類與更新](https://github.com/gaze9999/codex-setup/blob/main/docs/tool-updates.md)

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

完整接法:

- [核心 MCP](https://github.com/gaze9999/codex-setup/blob/main/docs/mcp.md)
- [開發工具](https://github.com/gaze9999/codex-setup/blob/main/docs/development-tools.md)
- [選用 MCP](https://github.com/gaze9999/codex-setup/blob/main/docs/optional-mcp.md)
- [中英日校對](https://github.com/gaze9999/codex-setup/blob/main/docs/proofreading.md)
- [UI / UX 工具](https://github.com/gaze9999/codex-setup/blob/main/docs/ui-ux.md)

公司電腦依允許的資料範圍選工具, credentials 使用環境的正式保存方式, 公司與私人帳戶分開設定

## 6. 更新已安裝工具

codex-tool-update 查選定工具的官方更新, 預覽後加 --apply 套用, 已授權的自動執行可加 --yes

```text
codex-tool-update --tool spartan
codex-tool-update --tool spartan --apply
```

將 spartan 換成要更新的工具 ID, 實際可更新項目見 [更新說明](https://github.com/gaze9999/codex-setup/blob/main/docs/tool-updates.md), setup wheel 在安裝它的獨立 venv 更新, venv 是該 Python 工具專用的環境

Desktop, CLI 與 plugin 使用各自官方更新通道, 專案 Framework 與 library 依該專案相容版本更新, 更新後重新載入並執行代表操作

Windows 更新 CLI 後確認命令位置與版本, 調整 PATH 前先備份並保留其他路徑, 重新開啟終端機或 App 以讀取新的環境

## 7. 套用介面中的設定

[Desktop 設定來源](https://github.com/gaze9999/codex-setup/tree/main/desktop) 保存 commit 與 PR 等提示詞, renderer 可產生設定片段, 再貼入對應介面或合併支援的設定

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
