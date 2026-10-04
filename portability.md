# 換電腦與本機鏡像

公開 repository 保存可攜的來源, 本機 Codex 目錄保存安裝鏡像, 方向固定由來源往鏡像, 永久變更先回來源審查

本文件介紹操作順序, installer, Skill ZIP 與 validator 由 [codex-setup](https://github.com/gaze9999/codex-setup) 維護 使用前閱讀該 checkout 的 README 與 script help, 不把這裡的示例視為執行權限

## 1. Clone 與確認來源

在自己選擇的工作目錄 clone 兩個公開 repository:

```text
git clone https://github.com/gaze9999/codex-playbook.git
git clone https://github.com/gaze9999/codex-setup.git
```

確認 remote, branch, revision 與 working tree, 記錄此次使用的來源版本, 要宣稱最新遠端狀態時需實際查遠端, 不能只看 cached tracking ref

Playbook 可直接閱讀, codex-setup 中的指示與 Skills 需另外安裝 Clone 不代表 global AGENTS.md 已生效, 也不代表 project role 或 session model 已切換

## 2. Global 指示與 model profile

在 codex-setup 根目錄使用既有 [global installer](https://github.com/gaze9999/codex-setup/blob/main/scripts/install_global_agents.py):

```text
python scripts/install_global_agents.py
python scripts/install_global_agents.py --install
python scripts/install_global_agents.py
```

不帶參數先比對, `--install` 安裝缺少或已相同的檔案, 若既有檔案不同則預設拒絕整批寫入 先人工合併, 明確要取代時使用 installer 的 `--replace` 並確認備份, 再比對一次

目標以 `CODEX_HOME` 或個人目錄中的預設 `.codex` 為準, 也可依 script help 指定替代目錄 此工具管理 global 指示與 subagent profile, 不覆寫既有 secrets, permissions, MCP 或完整 `config.toml`

Profile 安裝與啟用是兩件事, CLI 可依 codex-setup 的 [agents 說明](https://github.com/gaze9999/codex-setup/blob/main/agents/README.md) 使用 profile, 其他用戶端則核對支援方式 手動合併設定時保留原有設定, 不直接覆蓋整份 config

### 更新本機 Codex 的範圍

來源管理的 global, profile 與 Skills 先比對 codex-setup, 有獨立修改時保存內容並合併適用規則, 不以更新為由直接覆蓋整份個人設定. 專案角色沿用各自 repository, 不全部搬到 global

已安裝的 CLI 與 MCP 按官方來源逐項核對穩定版及相容性, 使用既有安裝方式更新, 未選用的工具維持未安裝. 專案相依的框架與工具仍配合專案版本, 不因本機更新改成全部使用最新版

Desktop, 獨立 CLI 與 plugin 有各自更新來源, 保留官方管理方式, 不手動覆寫 Desktop 內附 binary, .system 或 plugin 快取. Windows CLI 更新後核對命令解析位置與版本, 若調整使用者 PATH, 先備份並保留其他路徑, 既有 App 或終端可能需重新開啟才會讀到新的環境

檔案同步, 套件版本, 設定解析, client 載入與實際功能分開驗證. 更新通道無法確認是否有新版時保留具體限制, 不把查詢不可用或套件安裝成功當成所有本機工具都已最新

### Desktop 設定與可編輯 prompts

[Desktop 設定來源與操作說明](https://github.com/gaze9999/codex-setup/tree/main/desktop) 保存 commit, PR 與 PR watcher 的 Markdown prompt, 以及可攜的 memories / branch-prefix 偏好. 編輯來源後可用 renderer 產生經 TOML 檢查的片段, 再將 prompt 貼入對應 UI 或合併已支援的設定, renderer 不改現有 config, 不搬 secrets 或整份 app state

準備就緒自動合併與 Custom rules 等 UI 項目另依說明人工核對, 不猜未確認的 config key. ChatGPT 自訂指示, Project, 雲端記憶與 Work 寫作風格另依 [手動設定說明](web-settings.md) 套用, 不由本機 renderer 或 global installer 同步. 安裝來源不代表 UI 已套用或既有 session 已 reload, 換電腦後逐項確認. 記憶內容與私人權限規則留在個人環境, 不包含於公開 bundle

## 3. Custom Skills

從 [codex-setup README](https://github.com/gaze9999/codex-setup#安裝與同步) 選擇需要的 Skills, 使用用戶端支援的 repo path 或 release 組合包安裝方式, 新版 Skills 只發布 all-skills 組合包, 包內各 Skill 仍有獨立目錄, 可選取所需項目. 目錄同步只限此來源管理的 Skill, MCP wheel 與安裝 bundle 另依其用途發布

來源清單會變動, 不將安裝數量固定為成功條件 比對實際目錄與各 Skill metadata, 不覆寫 `.system`, plugin 或其他來源的 Skill

若本機鏡像不同, 先判斷是來源未同步還是鏡像存在獨立修改, 保存必要備份, 將永久修改合回來源, 再單向同步

在 codex-setup 根目錄驗證來源:

```text
python scripts/audit_skills.py
```

鏡像比對使用 audit 工具的 `--installed-root`, 指向這台機器的 Codex skills 目錄, 具體參數參考 [audit script](https://github.com/gaze9999/codex-setup/blob/main/scripts/audit_skills.py) 與 README 比對相對路徑與 hash, 不能只比目錄數量

## 4. MCP 與其他本機依賴

只安裝實際需要的工具, 核心 adapter 依 [MCP 安裝文件](https://github.com/gaze9999/codex-setup/blob/main/docs/mcp.md) 指定 runtime 與允許讀取的 roots, 其他工具依 [開發工具設定](https://github.com/gaze9999/codex-setup/blob/main/docs/development-tools.md), [選用 MCP 清單](https://github.com/gaze9999/codex-setup/blob/main/docs/optional-mcp.md) 與 [中英日校對設定](https://github.com/gaze9999/codex-setup/blob/main/docs/proofreading.md) 逐項選擇, 使用既有 installer 的預覽與套用機制

每個工具分開檢查平台, Python / Node / browser 或桌面 App 相依, API key, 帳戶授權及可用額度, 不因選一項就安裝全部. 只有 CLI 的工具沿用 CLI, 需 MCP 互動時才使用已有的 MCP 或 adapter. Hosted MCP 的帳戶授權, 僅保留接法的工具與實際可安裝項目分開核對, 不能把包內 recipe 當成已可呼叫

[用途分類與更新](https://github.com/gaze9999/codex-setup/blob/main/docs/tool-updates.md) 由 setup wheel 保存, `--profile development` 可在開發電腦篩選相關工具, 其他用途使用 design, office, research 或 personal, 每次仍選單一工具. `codex-tool-update --tool <tool>` 查選定工具的官方新版, `--apply` 套用, 已授權的自動執行可加 `--yes`, 不自行建立排程或擴張到未安裝工具. Setup wheel 更新在其獨立 venv 核對官方 release manifest 與 checksum, 不修改帳戶或專案 library

UI / UX 的研究來源, 設計 MCP, library 與無障礙工具依 [setup 接法](https://github.com/gaze9999/codex-setup/blob/main/docs/ui-ux.md) 選取, 流程判斷由 ui-ux-design Skill 處理, 不在通用 agent 指示固定 provider. Hosted / local Penpot 與免費 axe extension / 訂閱 MCP 的相依不同, 分別驗證

工作流程按缺少的能力選擇現有工具, 例如版本文件, 瀏覽器驗證, symbol / references, trace 或文字校對, 不在通用 Skill 固定 provider. 繁中依台灣詞表與半形標點, 英文依英文慣例, 日文保留日文標點及文體

安裝相依, 寫入 MCP 註冊, authentication, client discovery 與成功 tool call 分開驗證, 本機檔案一致不代表另一台電腦或雲端用戶端也可使用

依目前 script 與 Runtime requirements 核對 Python 等版本, 未確認前不替換 interpreter, 升級套件或修復整個環境 複製治理檔不會安裝 runtime 或授予 filesystem / network 權限

通用 CLI / Python 工具與可重用 core 由 [my-py-tools](https://github.com/gaze9999/my-py-tools) 維護, 可獨立於 Codex 使用, codex-setup 維護 Codex adapter 與安裝整合, 使用有版本的 core 套件 依各自來源核對版本與安裝要求, 不在 playbook 或 adapter 中複製 core

Authentication 與秘密資料依該環境的正式方式設定, 不放在 repository, prompt 或公開 log, 保留本機既有配置與外部服務選擇

Git author / committer identity 留在自己的 Git config, 個人與公司工作可依 repo local config 或實際工作區的 conditional include 分流, 換電腦重新核對路徑與有效設定. 個人 GitHub noreply email 從自己的帳號設定確認, 不把公司 email 或別人的署名複製到公開範例

發布前先建立適合專案的 gitignore, 核對待提交內容與 author / committer. 身分設定只影響後續提交, 不會自動改寫歷史, 若明確授權歷史改寫, 先備份, 核對協作者與 refs, 以已知遠端值保護推送, 再核對 tags / releases / attribution. 不因更換身分擴張到其他 repo 的歷史

## 5. Project preflight

- 閱讀 project root 與 nearest nested AGENTS.md, 確認實際 runtime, commands, public interfaces 與 ownership
- 查驗 branch / HEAD, dirty / untracked 檔案, ignored 指示, 必要規格與目前 progress record
- 核對 Main 與 child 的可用 model / effort, defaults, role pins 與實際 session, 不以檔案 parse 成功宣稱已 reload
- 確認 formatter 與 focused checks 所需依賴, 記錄缺少項目與證明範圍
- 在新 checkout / worktree 確認必要本機資料, shared services 與 mutable resources, 再開始寫入

## 6. 完成比對後記錄

保留 source revision, 目標鏡像, hash / audit 結果, 配置變更與未驗證項目, 個人路徑留在私有 progress record

Source / mirror 一致只證明此次檔案內容一致, Skill discovery, role reload, runtime, network, API 與 release 仍需各自的實際證據 這份 playbook 的文件檢查不代表上述安裝流程已在所有平台執行
