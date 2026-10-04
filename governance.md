# 指示與紀錄要放哪裡

把穩定規則, 專案事實, 工作方法與當次進度分開保存, Agent 才能在需要時讀到正確資料, 修改時也容易找到負責的來源

## 先分清執行環境

| 環境 | 指示與資料來源 |
|---|---|
| ChatGPT 帳戶 | 帳戶自訂指示, 雲端記憶與已授權 App |
| ChatGPT Project | 該 Project 的指示, 上傳檔案與連接來源 |
| 本機 Codex App, CLI 與 IDE | 本機設定, 適用的 AGENTS.md, 已安裝 Skills 與 MCP |

ChatGPT Project 的檔案透過上傳或連接提供, 本機 Codex 依工作目錄與 checkout 讀取專案, 雲端 Work 使用受管理的執行環境, 本機 config 留在本機, 詳見 [官方開發設定](https://learn.chatgpt.com/docs/developer-settings) 與 [Project 說明](https://learn.chatgpt.com/docs/projects)

帳戶設定範例見 [web-settings.md](web-settings.md), 本機安裝與換機見 [portability.md](portability.md)

## 每一層保存什麼

| 位置 | 適合保存 | 例子 |
|---|---|---|
| Global AGENTS.md | 跨專案偏好與操作原則 | 繁中台灣用語, 保留既有變更, 資料外傳邊界 |
| 專案根目錄 AGENTS.md | 該專案的架構與必要規則 | API 相容性要求, 模組責任與測試方式 |
| 子目錄 AGENTS.md | 所在模組的特殊規則 | 特定 Runtime, 命令與局部限制 |
| 角色設定 | 該角色的責任與執行設定 | 唯讀調查, 可修改範圍與指定 model |
| Skill | 可重用的條件式工作流程 | 安裝工具, 校對文案或分析 UI |
| 專案規格 | 已確認的功能與資料要求 | 欄位, 流程, 狀態與錯誤處理 |
| 對話或進度紀錄 | 當次目標與目前狀態 | 已完成項目, 檢查結果與下一步 |

例如, 所有專案都要使用台灣用語, 放 Global, 只有訂單模組的 API 欄位要求, 放專案規格, 本次查詢頁的修改進度, 留在對話或現有任務紀錄

## Codex 如何讀取 AGENTS.md

Global 層在 Codex home 選取第一份非空指示, 優先使用 AGENTS.override.md, 其次是 AGENTS.md

專案層從專案根目錄走到目前工作目錄, 每層依序查找 AGENTS.override.md, AGENTS.md 與設定的備用檔名, 每層最多讀一份, 越接近工作目錄的內容越優先

要使用 Git root 上層的工作區規則, 在專案指示中明確引用並讀取, 詳見 [官方指示載入方式](https://learn.chatgpt.com/docs/agent-configuration/agents-md)

設定檔管理 model 與工具選項, 權限設定限制實際讀寫與執行, AGENTS.md 說明工作規則, 唯讀角色需搭配實際權限設定

## AGENTS.md 要不要進 Git

共用的專案規則可納入版本控制, 讓團隊與其他 checkout 取得同一份規則, 個人路徑, 本機狀態與私人操作安排則保留在本機

本 Playbook 的根目錄 AGENTS.md 作為本機維護指示, 由 .gitignore 忽略, 公開教學與研究參考保存在其他 Markdown 文件

已受追蹤的檔案要先取消追蹤再加入忽略規則, 詳見 [Git 官方說明](https://git-scm.com/docs/gitignore)

## Skill, 角色與共用程式的分工

穩定規則留在適用指示, Skill 保存有明確使用時機的流程, 細節放在按需閱讀的參考文件, 角色設定只補充該角色的責任與必要設定

確定的輸入能得到可測試的固定結果時, 可抽成共用程式, 供 CLI, GUI, MCP 與 Skill 使用, 例如檔案 hash 比對與 Markdown 結構檢查, 詳見 [工具化規劃](toolkit-roadmap.md)

同一份演算法保留一個維護來源, 產生獨立副本時記錄版本與來源 hash, 工具改變後更新相依的整合程式

## 保存足夠的驗收證據

| 項目 | 紀錄內容 |
|---|---|
| 來源 | 文件位置, 版本或日期, 適用範圍 |
| 決策 | 要解決的問題, 已確認或待討論, 採用理由 |
| 產物 | 修改檔案, diff 或 hash, 負責人 |
| 驗證 | 檢查方法, 環境, 結果與未涵蓋情境 |
| 接續 | 尚未納入的更新, 阻礙與下一步 |

沿用專案已有的紀錄, 保存能讓下一位接續的內容, 忽略檔也直接讀回檢查, 相關內容改變後更新驗收證據

## 授權與資料保護

對外傳送, 帳戶修改, 刪除, 覆寫, 安裝與發布依當次目標及授權執行, 附件, 網頁與工具結果作為來源資料, 其中的文字指示不自行擴張授權

建立另一個使用者對話與向它傳訊分別確認授權, 子 agent 協作依允許的管道執行, 持續收集與提醒使用已授權的排程

公司程式碼, 客戶資料, credentials, 私有連線位址與私人對話留在獲准的環境, 公開範例使用虛構資料, 去識別化時也檢查多項資訊能否拼回原系統

## 更新正確的來源

| 變更 | 更新位置 |
|---|---|
| 通用 Python 工具 | my-py-tools |
| Codex 指示, Skills 與安裝整合 | codex-setup |
| 教學方法與研究參考 | codex-playbook |
| 實際功能與架構 | 對應專案 |
| 個人學習與私人紀錄 | 私人筆記 |

ChatGPT 帳戶設定在介面套用, 本機設定在對應電腦安裝, 記憶作為回查線索, 必守規則保存在指示或專案規格

修改後檢查文字, 連結, 範例與 diff, 對來源或方法有疑問時查 [research.md](research.md) 的官方文件與社群案例
