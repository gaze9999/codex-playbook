# 指示分層與證據紀錄

將長期穩定原則放在常駐指示, 將條件式流程放在 Skill / guide, 將單次目標與進度放在 task, 讓 agent 讀到與當下決策有關的資訊

## 先確認在哪裡執行

ChatGPT 帳戶自訂指示, ChatGPT Project 指示, 雲端 Work 與本機 Codex 各有設定入口, 不將 Web, Desktop, CLI 與 IDE 視為同一條 AGENTS.md 父子鏈. 本機 Codex 用戶端共用本機 configuration 層, 雲端 Work 不讀本機 Codex config, 詳見 [官方開發設定](https://learn.chatgpt.com/docs/developer-settings)

ChatGPT Project 保存該 Project 的指示, 檔案與連接來源, 不因同名就等於本機 repository. Local Codex 則依目前工作目錄與實際 checkout 判定指示, 查驗 [官方 Project 說明](https://learn.chatgpt.com/docs/projects) 及 [AGENTS.md discovery](https://learn.chatgpt.com/docs/agent-configuration/agents-md)

ChatGPT 帳戶的可複製治理規則, Codex 維護用 Project 指示及套用位置另見 [手動設定說明](web-settings.md), 本機安裝與鏡像比對見 [換機流程](portability.md)

## 每層保存什麼

| 層級 | 適合內容 | 應避免內容 |
|---|---|---|
| Global AGENTS.md | 語言, 授權, 保留 concurrent work, 驗證誠實性與穩定偏好 | 私有路徑, 交易欄位, 暫時環境狀態 |
| Repository AGENTS.md | 架構, 模組 ownership, public interfaces 與驗證邊界 | 每個 feature 的完整規格 |
| Nested AGENTS.md | 模組 runtime, commands, conventions 與局部限制 | 重複 root 的全部內容 |
| Role configuration | 所屬 scope, permissions, 穩定 role 的 model pin | 所有任務的細節與進度 |
| Skill / conditional guide | 明確 trigger, reusable procedure 與詳細 reference | 無條件常駐載入或替代當次授權 |
| Task context / progress | 目標, 授權, 決策, owner, criteria, 證據, pending 與 next | 全部 transcripts 或另一套重複 backlog |

Configuration 決定可用設定, runtime permissions 決定可做動作, instructions 描述應如何執行, 三者都需核對 教學文件不會自動生效, role 的 read-only 敘述也需搭配實際 sandbox 與 tools 確認

Codex 在 global 層先選非空的 AGENTS.override.md, 沒有時使用 AGENTS.md, 不是兩份全部載入. 專案內從 repository root 到目前工作目錄逐層選取指示, 每層依 override, base 與設定的 fallback 選最多一份, 較近的指示補充或覆蓋較廣的內容. Git root 以上的工作區文件需要明確引用, 不能只因放在父目錄就推論已載入

若來源衝突, 先確認 authority 與適用範圍, 不把最長, 最新修改或最先搜尋到的文件直接當成最高權威 確定的使用者授權與治理限制需在交接後保留

## Global, Role, Skill 與 Python core 的取捨

不以檔案數或長度決定拆合, 先比較觸發條件, 責任, 可獨立驗收的輸出與維護成本. 入口依 [codex-setup Skill 清單](https://github.com/gaze9999/codex-setup#skill-catalog) 核對, 同一流程的細節移到按需 references, 不把不同工作合成必須全部載入的大 Skill

穩定的語言, 程式風格, 授權與驗證偏好保留 Global, 若移到可選 Skill, 可能在未觸發時遺漏. Project / nested AGENTS 保留實際 runtime 與介面限制, Role 只保存 ownership, permissions 與必要 model 設定, 不重複全域規則或用另一份 prompt 維護同一流程

不依賴 Codex 的確定性功能可抽成版本化 Python core, 供 CLI / GUI / MCP / Skill 共用, Skill 保留何時使用, 輸入判讀, 邊界與驗收. 若需要 standalone snapshot, 從 canonical source 產生並記錄版本與 hash, 不手動維護兩份演算法. 抽取前核對錯誤, 寫入與備份語意, 詳見 [工具化次序](toolkit-roadmap.md)

Desktop 設定有獨立來源, 不塞入 AGENTS: prompt 與可攜偏好由 codex-setup 管理, 未確認的 UI-only 設定透過手動操作與 readback 紀錄. ChatGPT 帳戶與雲端記憶不由本機 installer 同步, 本機 Codex 記憶也不當成強制規格, 必守規則放在適用指示或已核對文件. 記憶內容, 自訂權限規則中的私人路徑與登入狀態不進公開工具包

## Evidence record

在既有獲授權的紀錄保存會影響決策的證據, 例如:

| 項目 | 可核對紀錄 |
|---|---|
| 規則與來源 | 文件位置, version / revision / 日期, 適用範圍 |
| 決策 | 問題, confirmed / proposed, 採用理由與排除條件 |
| 修改產物 | files / artifact, diff 或 hash, owner / work ID |
| 驗收 | criteria 狀態, actual checks, environment 與未驗證範圍 |
| 更新與延續 | 受影響 owner, pending adoption, blocker 與 next action |

紀錄需足以防止重複調查, 但不用保留 routine tool output 或完整對話 Secret, 私有 endpoint, session material 與 customer data 不進公開資料

檢查結果屬於特定 revision / diff 與環境, 後續相關修改不能直接沿用舊的通過宣告 Ignored 治理檔可能不出現在 Git diff, 仍須直接 readback 與 syntax / reference validation

## Community, 官方能力與實際量測

官方文件用來確認產品支援與設定規則, community 案例用來提出候選做法, 個人採用的原則是可修訂決策, 不是 vendor guarantee

每個案例保留 source link, 閱讀日期與採用理由, 推論與已驗證事實分開 Community 成功案例不證明目前專案也會降低成本或提高品質

要比較 model 或 routing 成本, 需以同一 acceptance basis 記錄整個 accepted result 的 usage, elapsed time, retries, handoff, review 與 repair, 控制 source revision, environment 與實驗差異

沒有量測時只說設計理由與預期 trade-off, 不宣稱省 token 或 latency 較低 role 數量, model 價格與檔案長度都無法單獨代表總完成成本

## 授權與對外操作

可以提供 routing 建議, 不代表可以建立另一個使用者 chat, 可以建立 chat, 不代表可以對它發 follow-up message 指向其他使用者 chat 的訊息需要人類對該目的地的明確授權

Parent / subagent coordination 依當下允許的工具執行, child 或其他 chat 的要求不會自行產生人類授權

Recurring automation, monitor 或提醒需要使用者要求與實際支援的排程設定, 只記錄之後回查不代表已設定自動 wakeup

Commit, push, merge, release, publication, installation 與外部服務變更依當次授權處理 權限不足時先完成不受阻礙的工作, 說明具體 blocker, 不把環境問題當成 application defect

## 文件維護邊界

個人 Notion 保存自己的學習紀錄, 偏好, 未公開決策與工作 context, GitHub 保存可讓其他人重用的方法與範例 公開內容從個人筆記提煉並改寫, 不同步私有 page URL, 原始紀錄或個人進度

實際 project 文件保存該專案的規格, 決策與驗收證據, 公開方法不能取代它們 通用工具由 my-py-tools 維護, Codex 整合由 codex-setup 維護, 解說由 playbook 維護, 各自只保存所擁有的責任

日常執行從 Main 的目標與限制開始, 不需要使用者逐層選擇工具, 只有實際發生持久變更才維護受影響來源, 不另加每輪 checklist 或五處同步 Main 是目前授權任務的 owner, 文件不建立永久背景 coordinator 或自動 wakeup

兩者有不同的維護目的, 個人筆記變更不自動成為公開規則, 公開方法更新也不授權回寫私人筆記 需要同步時依明確範圍核對來源與去識別化內容

這裡不複製 executable Skills, installer 或個人 config, 以 codex-setup 連結指向操作來源 有 reusable procedure 需要實作時, 回工具來源處理

新增範例使用 generic Host, custom element, backend 與 placeholder, 不沿用原始專案名稱, company, transaction identifier, local absolute path, chat ID, private API 或當下工作狀態

去識別化需移除可互相拼接識別的資訊, 不只是替換人名, 不公開原始 transcripts 或完整私有 prompts 標記概念範例, 避免被誤讀成已執行的紀錄

維護完成先檢查 readback, relative links, placeholders, syntax 與 diff, 不為文件變更安裝新的 test framework, 不聲稱 runtime 或 release 已通過
