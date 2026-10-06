# Codex Playbook

這份指南說明如何用 Codex 完成開發工作, 從提出需求, 查閱專案, 修改程式到驗收成果, 也整理換電腦, 維護設定與研究新工具的方法

第一次使用時, 先完成一個小功能, 確認整個流程跑得通, 再加入分工或額外工具

## 第一次使用

1. 在目標專案開啟 Codex, 說明要完成的功能與可修改範圍
2. 提供規格或現有畫面, 用一個操作情境說明預期結果
3. 讓 agent 讀取專案指示與相關實作, 確認技術棧及目前變更
4. 修改後檢查實際畫面或資料, 對照需求驗收

例如, 要改善訂單查詢, 可以直接說:

```text
請改善訂單查詢頁

輸入有效的訂單編號後顯示訂單狀態, 查無資料時顯示清楚的提示, 查詢失敗時保留輸入並提供重試
先參考目前專案的表單與錯誤處理方式, 保留既有 API 格式與其他人的變更
完成後驗證這三種情境, 回報修改內容與檢查結果
```

完整操作方式見 [開發流程](workflow.md), 其他任務可使用 [提示詞範例](prompts.md)

## 先理解幾個名詞

| 名詞 | 在這份指南中的意思 |
|---|---|
| Agent | 能依指示閱讀資料, 使用工具並完成工作的 AI 助理 |
| Main | 主 agent, 負責理解需求, 決策, 整合與最終驗收 |
| Subagent | 子 agent, 接手範圍明確的部分工作, 完成後回報 Main |
| 負責人 (owner) | 負責完成某項工作並提出驗收證據的人或 agent |
| Context | Agent 目前用來判斷的資料, 包含需求, 規格, 程式碼與先前決策 |
| AGENTS.md | Codex 讀取的文字指示, 用來保存共用偏好或專案規則 |
| Skill | 可重用的工作流程, 說明何時使用, 怎麼執行與如何驗收 |
| Plugin | 組合 Skills、MCP 或 app 能力的套件, 安裝與帳戶連接依目標用戶端處理 |
| MCP | 讓 agent 連接工具與外部系統的協定, 例如查文件或操作瀏覽器 |
| CLI | 在終端機執行的工具, Agent 也可以透過命令使用 |
| 驗收條件 | 能觀察或檢查的完成標準, 例如輸入, 操作與預期結果 |
| Worktree | 同一個 Git repository 的另一份工作目錄, 可供不同分支各自修改 |
| Repository | Git 管理的專案存放庫, 保存檔案與修改歷史 |

AGENTS.md 與 Skill 提供工作指示, MCP 與 CLI 提供執行能力, 工具的安裝與接法集中在 [codex-setup](https://github.com/gaze9999/codex-setup)

## 依需求閱讀

| 你現在要做什麼 | 閱讀入口 |
|---|---|
| 完成一個功能或修正問題 | [開發流程](workflow.md) |
| 複製 coding prompt, 對照預期交付與回報示意 | [提示詞範例](prompts.md) |
| 換電腦, 安裝 Skills 或連接 MCP | [安裝與換機](portability.md) |
| 決定規則, 規格與進度要放哪裡 | [指示與紀錄管理](governance.md) |
| 將對話中的方法整理成可重用教學 | [對話轉教學](governance.md#從對話提煉教學), [提示詞範例](prompts.md#從目前對話整理教學) |
| 納入中途更正並恢復未完成工作 | [中途修正](workflow.md#8-納入中途修正), [補充需求範例](prompts.md#中途補充與更正) |
| 設定 ChatGPT 帳戶或維護用 Project | [帳戶與手動設定](web-settings.md) |
| 查來源, 理解採用理由或準備教學 | [研究參考](research.md) |
| 評估資料的閱讀順序或分類 | [Jev 使用時機](jev.md) |
| 持續研究新技術與安排學習 | [知識追蹤](knowledge-radar.md) |
| 檢查應用程式的安全風險 | [紅隊檢查](red-team.md) |
| 決定新增 Skill 或抽出通用工具 | [工具化規劃](toolkit-roadmap.md) |
| 選擇 Skill、CLI、MCP 或 Plugin | [工作能力與介面選擇](toolkit-roadmap.md#按任務選工具介面) |
| 比較遊戲策略、成長節奏與隨機獎勵 | [遊戲數值與模擬](game-balance.md) |

先讀與目前任務相關的頁面, 詳細資料在需要時再補

## 各份資料的用途

| 位置 | 保存內容 |
|---|---|
| [my-py-tools](https://github.com/gaze9999/my-py-tools) | 可獨立使用的 Python 工具與共用程式 |
| [codex-setup](https://github.com/gaze9999/codex-setup) | Agent 治理來源、自訂 Skills、Plugin 管理入口及 MCP 安裝整合 |
| codex-playbook | 教學, 判斷理由與可複製範例 |
| 專案文件 | 該專案的規格, 架構, 決策與驗收紀錄 |
| 私人筆記 | 個人學習紀錄, 未公開工作與私人資料 |

平常從 Main 開始, 把目標與限制說清楚即可, Agent 依工作需要選擇流程與工具, 有持久變更時再更新對應來源

## 維護方式

工作方法與範例在這裡更新, 安裝工具與可執行 Skills 回到 codex-setup 更新, 研究來源與教學依據保存在 research.md

更新前對照 setup 的 [文件索引](https://github.com/gaze9999/codex-setup/blob/main/docs/README.md) 與目前實作, 先修正失效入口, 再補使用時機、判斷方式與驗收範例, 選材方式見 [從來源更新教學](governance.md#從-codex-setup-選擇教學內容)

本 repository 以 main 分支文件作為目前版本, 檢查後依授權 commit 與 push, 需要固定引用時使用 commit permalink
