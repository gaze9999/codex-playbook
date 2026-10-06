# 指示與紀錄要放哪裡

把穩定規則, 專案事實, 工作方法與當次進度分開保存, Agent 才能在需要時讀到正確資料, 修改時也容易找到負責的來源

## 先分清執行環境

| 環境 | 指示與資料來源 |
|---|---|
| ChatGPT 帳戶 | 帳戶自訂指示, 雲端記憶與已授權 App |
| ChatGPT Project | 該 Project 的指示, 上傳檔案與連接來源 |
| 本機 Codex App, CLI 與 IDE | 本機設定、適用的 AGENTS.md、已安裝 Skills、Plugins 與 MCP |

ChatGPT Project 的檔案透過上傳或連接提供, 本機 Codex 依工作目錄與 checkout 讀取專案, 雲端 Work 使用受管理的執行環境, 本機 config 留在本機, 詳見 [官方開發設定](https://learn.chatgpt.com/docs/developer-settings) 與 [Project 說明](https://learn.chatgpt.com/docs/projects)

帳戶設定範例見 [web-settings.md](web-settings.md), 本機安裝與換機見 [portability.md](portability.md)

修改後依各環境分別記錄檔案已保存, 設定已套用, 帳戶已授權與實際呼叫結果, 需要手動操作的項目列出位置與下一步, 用對應證據確認生效

## 每一層保存什麼

| 位置 | 適合保存 | 例子 |
|---|---|---|
| Global AGENTS.md | 跨專案偏好與操作原則 | 繁中台灣用語, 保留既有變更, 資料外傳邊界 |
| 專案根目錄 AGENTS.md | 該專案的架構與必要規則 | API 相容性要求, 模組責任與測試方式 |
| 子目錄 AGENTS.md | 所在模組的特殊規則 | 特定 Runtime, 命令與局部限制 |
| 角色設定 | 該角色的責任與執行設定 | 唯讀調查, 可修改範圍與指定 model |
| Skill | 可重用的條件式工作流程 | 安裝工具, 校對文案或分析 UI |
| 專案規格 | 已確認的功能與資料要求 | 欄位, 流程, 狀態與錯誤處理 |
| 對話的 task context | 當次原始需求、後續引導與目前狀態 | 有效決策、已完成項目、待驗收與下一步 |

例如, 所有專案都要使用台灣用語, 放 Global, 只有訂單模組的 API 欄位要求, 放專案規格, 本次查詢頁的修改進度, 留在對話或現有任務紀錄

## Codex 如何讀取 AGENTS.md

Codex 在啟動時建立指示鏈, 核對目前工作目錄, 實際來源與設定的大小限制, 確認適用指示已載入

Global 層在 Codex home 選取第一份非空指示, 優先使用 AGENTS.override.md, 其次是 AGENTS.md

專案層從專案根目錄走到目前工作目錄, 每層依序查找 AGENTS.override.md, AGENTS.md 與設定的備用檔名, 每層最多讀一份, 越接近工作目錄的內容越優先

要使用 Git root 上層的工作區規則, 在專案指示中明確引用並讀取, 同時保留單獨 clone 時足以工作的專案規則, 詳見 [官方指示載入方式](https://learn.chatgpt.com/docs/agent-configuration/agents-md)

設定檔管理 model 與工具選項, 權限設定限制實際讀寫與執行, AGENTS.md 說明工作規則, 唯讀角色需搭配實際權限設定

## AGENTS.md 要不要進 Git

共用的專案規則可納入版本控制, 讓團隊與其他 checkout 取得同一份規則, 個人路徑, 本機狀態與私人操作安排則保留在本機

本 Playbook 的根目錄 AGENTS.md 作為本機維護指示, 由 .gitignore 忽略, 公開教學與研究參考保存在其他 Markdown 文件

已受追蹤的檔案要先取消追蹤再加入忽略規則, 詳見 [Git 官方說明](https://git-scm.com/docs/gitignore)

## Skill, 角色與共用程式的分工

穩定規則留在適用指示, Skill 保存有明確使用時機的流程, 細節放在按需閱讀的參考文件, 角色設定只補充該角色的責任與必要設定

確定的輸入能得到可測試的固定結果時, 可抽成共用程式, 供 CLI, GUI, MCP 與 Skill 使用, 例如檔案 hash 比對與 Markdown 結構檢查, 詳見 [工具化規劃](toolkit-roadmap.md)

同一份演算法保留一個維護來源, 產生獨立副本時記錄版本與來源 hash, 工具改變後更新相依的整合程式

## 新專案的 agent 規劃

先讀實際專案、設定與現有指示, 再選 [Project starter](https://github.com/gaze9999/codex-setup/blob/main/skills/agent-governance/assets/project-starter/README.md) 中需要的範本, 專案層補充會影響該專案工作的事實, 來源範本與目前生效的指示分開核對

| 層級 | 要保留的內容 | 建立條件 |
|---|---|---|
| root AGENTS.md | 模組責任、公開介面、Git 慣例與最小足夠驗證 | 專案共同規則需要持久保存 |
| nested AGENTS.md | 所在模組的 runtime、實作模式與驗收差異 | 模組有不同責任或限制 |
| 條件式 guide | 功能規格導覽、分流、進度與歷史更新方式 | 只有相關任務才需要的詳細程序 |
| subagent role | 具體問題、可修改範圍、權限與預期回傳 | 已允許委派且工作可獨立驗收 |
| task context | 本次需求、有效決策、owner、相依與未完成事項 | 當次執行與接續 |

Main 保留需求、跨模組決策、必要直接實作、整合與最終驗收, 先沿用合適的既有角色, 規劃角色時保留同一功能的修改與檢查責任, shared interface 未確認前先處理相依, model 與 effort 依目前支援和工作不確定性判定

以有 Backend、Host 與 custom element 的架構為例, Host 管理 session、導覽、權限與載入, 功能 UI 留在對應 custom element, payload、properties / events、路由、bundle 與共用資產由相關 owner 確認, 此例適用條件與指令見 [去識別化專案範本](https://github.com/gaze9999/codex-setup/blob/main/skills/agent-governance/assets/project-starter/examples/host-and-custom-elements/AGENTS.md)

專案需要進度與歷史文件時, 先確認位置與觸發條件, 可以採用以下方式:

- 有實質應用修改或會改變進度的新驗證時, 更新受影響進度並追加一則有日期的歷史
- 有決策、阻礙或下一步變更時, 更新相關狀態, 需要回溯才保留前後決策與原因
- 治理、工具或純文件修改只更新已授權文件, 應用進度依實際成果判定
- 保留既有問題 ID, 已解決項目可用 `~~ISSUE-01~~` 並留下修正與證據, 新 ID 依專案既定順序配置
- 紀錄使用專案約定的時區與分鐘時間戳記, 有相關且已核對的 commit 才附短 SHA 與具體變更, 未提交內容另外標明

這些是可採用的專案紀錄方式, 每輪對話結束本身不要求追加歷史, 詳細範例見 [records guide](https://github.com/gaze9999/codex-setup/blob/main/skills/agent-governance/assets/project-starter/examples/host-and-custom-elements/.codex/agent-guidance/records.md)

套用前移除私有路徑、公司或交易識別資訊, 用實際已確認內容取代待填欄位, 核對 root 與目標模組的指示鏈、大小限制、角色 TOML、權限與忽略檔, 新 worktree 另確認本機指示是否存在, 最後在目標環境核對載入, 文件解析成功只證明檔案格式

## 保存足夠的驗收證據

| 項目 | 紀錄內容 |
|---|---|
| 來源 | 文件位置, 版本或日期, 適用範圍 |
| 決策 | 要解決的問題, 已確認或待討論, 採用理由 |
| 產物 | 修改檔案, diff 或 hash, 負責人 |
| 驗證 | 檢查方法, 環境, 結果與未涵蓋情境 |
| 接續 | 尚未納入的更新, 阻礙與下一步 |

優先在目前對話保存能讓下一位接續的有效狀態, 只有明確要求或專案既有規範才更新允許位置的進度文件, 忽略檔也直接讀回檢查, 相關內容改變後更新驗收證據

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

修改後檢查連結, 範例, 程式碼區塊與 diff, 對新增或修改文字執行可用的 textlint 或同等檢查, 再人工複核語意與台灣用詞, 工具缺少, 不適用或失敗時回報未完成檢查的範圍與原因

規格定義的標題, 欄位, 按鈕, 狀態, 提示文字與標點保留原文, 校對前先辨識這些文字與程式碼, 引用及 symbol, 逐項對照 lint 建議的修改範圍與來源, 規格文案變更需有明確授權

對來源或方法有疑問時查 [research.md](research.md) 的官方文件與社群案例

## 從 codex-setup 選擇教學內容

先對照目前 [文件索引](https://github.com/gaze9999/codex-setup/blob/main/docs/README.md)、相關 diff 與 Playbook 章節, 依對讀者的影響選擇更新, 來源尚在重整時核對目前檔案, 以來源檢視說明可確認的內容

| setup 來源 | 可轉成教學的內容 | Playbook 位置 |
|---|---|---|
| [Agents](https://github.com/gaze9999/codex-setup/blob/main/docs/agents.md) 與治理參考 | 規則放哪裡、如何延續需求、回報與驗收 | 本頁、workflow.md、prompts.md |
| [Skills](https://github.com/gaze9999/codex-setup/blob/main/docs/skills.md) 與相關 SKILL.md | 使用時機、預期產物、相依與常見判斷 | toolkit-roadmap.md 及對應主題 |
| [MCP](https://github.com/gaze9999/codex-setup/blob/main/docs/mcp.md) 與工具文件 | 依能力選介面、帳戶與資料範圍、代表性呼叫 | portability.md、toolkit-roadmap.md |
| [Plugins](https://github.com/gaze9999/codex-setup/blob/main/docs/plugins.md) | 套件、Skill 鏡像與帳戶連接的管理方式 | portability.md、toolkit-roadmap.md |
| [安裝與管理](https://github.com/gaze9999/codex-setup/blob/main/docs/setup/cli.md) 與使用教學 | 操作順序、有效入口與故障判讀 | portability.md、jev.md 及對應主題 |

可重用且有來源支持的方法納入教學, 技術版本、完整工具清單、安裝實作與參數由 setup 維護並連回來源, 個人設定值與一次性的操作紀錄留在所屬環境

已經涵蓋的原則保留, 名稱、路徑或行為改變時更新受影響段落與引用, 新主題需要獨立閱讀時才新增教學頁, 規則範本說明如何採用, 實際操作結果依對應版本與環境的證據回報

## 從對話提煉教學

先把對話中的有效決策與既有文件對照, 再補上缺少的判斷方法, 操作步驟與範例, 已有章節能承接時直接修改, 主題需要獨立閱讀時才新增文件

| 對話內容 | 適合保存的位置與形式 |
|---|---|
| 穩定偏好或必守邊界 | 適用的 agent 指示, 教學補充理由與使用方式 |
| 可重複使用的操作流程 | Playbook 的方法與範例, 可執行部分由工具來源維護 |
| 已確認的專案規格與決策 | 專案文件, 公開教學保留去識別化的判斷方法 |
| 單次進度, 失敗與檢查結果 | 原有對話或進度紀錄, 教學提煉可重現的條件 |
| 候選方案或待確認問題 | 保留條件與未知資訊, 取得決策後再更新相關內容 |

整理時依以下順序處理:

1. 確認目前可讀的對話, 使用者仍有效的要求與授權, 缺少的歷史只阻擋依賴該資訊的段落
2. 搜尋既有章節與相關來源, 分清使用者要求, 已確認決策, 作者建議與實際檢查結果
3. 說明何時使用, 如何判斷, 如何執行與如何驗收, 用通用模組與示例資料呈現必要情境
4. 移除可拼接識別的公司, 專案, 路徑, 私有連結, 對話 ID 與原始紀錄, 保留影響理解的相依與授權條件
5. 更新入口與相互引用, 執行文字與結構檢查, 對照實際 diff 確認沒有把一次結果寫成通用保證

以資料轉換的測試資料為例, 教學說明如何選擇代表輸入與比對結果, 專案進度保存該次檢查的版本與結果, 真實 API 與重新開啟後的資料保存, 各自使用對應的驗收情境與證據

需要完整檢視較早的對話時, 先確認是否有獲授權的歷史來源, 交付時說明實際讀到的範圍, 可複製的提示詞放在同一個完整 `text` 程式碼區塊, 工具或 model 建議放在區塊外, 範例見 [從目前對話整理教學](prompts.md#從目前對話整理教學)
