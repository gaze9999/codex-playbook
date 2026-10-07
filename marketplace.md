# 使用公開市集與獨立工具

[Codex Toolkit](https://github.com/gaze9999/codex-toolkit) 提供公開 Skills、Plugins、MCP 串接及 Python 工具. Playbook 說明使用情境與操作, 各項工具的版本、參數及相依由 Toolkit 維護

| 你需要什麼 | 用法 |
|---|---|
| Agent 工作流程 | 在支援的 Codex 用戶端加入市集, 選需要的 Plugin |
| 不用 Codex 執行工具 | 使用 Python CLI 或核心 wheel |
| 用戶端的結構化工具 | 安裝所需 MCP runtime, 另設帳戶與存取範圍 |
| 還原自己的電腦 | 在私人設定來源保存 profile, 使用公開安裝器預覽與套用 |

## 加入市集

在 Codex 外掛管理頁的市集入口加入 `gaze9999/codex-toolkit`, 或使用支援 Plugin 的 CLI:

```text
codex plugin marketplace add gaze9999/codex-toolkit
codex plugin list --marketplace codex-toolkit --json
codex plugin add codex-agent-workflow@codex-toolkit
```

Windows 若出現 `Filename too long`, Git for Windows 可啟用長路徑, 這項設定影響該使用者的 Git:

```text
git config --global core.longpaths true
```

也可從較短的來源路徑加入本機市集. 支援細節見 [Git for Windows 設定](https://github.com/git-for-windows/git/blob/main/Documentation/config/core.adoc)

先選一組符合工作目的的外掛, 檢查啟用條件、版本與相依. 已直接安裝的同名 Skill 或其他市集來源先選定 owner, 避免重複啟用. 安裝後在新對話確認載入, 再用代表性任務驗證

這份 Git 市集可自行加入, 官方公開目錄收錄另有提交程序. 市集提供的工作流程、MCP runtime、帳戶授權及真正工具呼叫各是不同步驟, 詳細操作見 [Toolkit 市集說明](https://github.com/gaze9999/codex-toolkit/blob/main/docs/marketplace.md), 原生能力依 [OpenAI Plugin 指引](https://developers.openai.com/plugins/build/plugins) 與目前用戶端版本確認

## Python 可以單獨使用

直接取得公開來源即可, 不需 Codex、Plugin 或 MCP:

```text
git clone https://github.com/gaze9999/codex-toolkit.git
python codex-toolkit/python-tools/launch-cli.py --list
python codex-toolkit/python-tools/launch-cli.py documents.convert_to_markdown --help
python codex-toolkit/python-tools/launch-cli.py documents.convert_to_markdown sample.txt --output-dir output --dry-run
```

CLI 需要 Python 3.10+, PDF / Office、精確 token 計算等功能再安裝所需相依. 完整 `python-tools/` 與授權檔可獨立保留, 也能安裝文件或工作區 core wheel 供自己的 Python 程式呼叫. 不只取一個依賴其他檔案的 helper, 不搬用戶端 cache 或另一台電腦的 venv

參考 [獨立使用說明](https://github.com/gaze9999/codex-toolkit/blob/main/python-tools/docs/standalone.md), [Python CLI](https://github.com/gaze9999/codex-toolkit/blob/main/python-tools/README.md) 與核心 API 文件

## 保存自己的選用項目

將個人 Global / 角色來源、選用 Skills / Plugins、平台工具與已核對 revision 存在自己的私人設定 repository, 只保存憑證變數名稱, 值由目標電腦安全提供. 還原時先預覽, 處理既有內容差異, 再逐項套用

工具執行邏輯保留一份公開來源, 私人設定用 profile 引用, Playbook 只保存跨專案教學. 範例與詳細還原入口見 [Toolkit Profile 指引](https://github.com/gaze9999/codex-toolkit/blob/main/docs/restore.md), 換機步驟見 [安裝與換機](portability.md)
