# 可依任務刪減的 prompt

以下是抽象範例, 不是每輪必貼的固定 boilerplate 方括號內容需換成實際資料; 適用且已確認的 project 指示可引用, 不再抄入每個 prompt

Prompt 說明此次目標, 權限, ownership 與驗收, 不用長篇風格指令掩蓋未確認需求 Model 建議放在 prompt 外, 並依當下 configuration 與支援程度選擇

## 直接執行

適合同一 owner 可以完成 discovery, edit 與驗證的工作 若只要 plan 或 review, 應改寫交付類型, 避免暗示實作授權

```text
請在 [repository / 目前 checkout] 完成 [具體可觀察結果]

先閱讀適用的 AGENTS.md, [來源指引] 與相似實作, 核對目前設定, Git status / diff 與其他人的變更
來源: [規格 / API / source pointers 與適用範圍]
已確認決策: [目前有效決策; 沒有則省略]
可修改: [功能 / 模組 / 檔案與行為]
保留: [公共介面, 相容性要求與 concurrent work]
排除: [明確不在本次範圍的工作]

驗收: [情境, 輸入與預期結果]
依 diff 與改變行為選最小且足夠的既有 checks, 保留必要 gate
缺少資訊只阻擋依賴部分; 繼續獨立且已授權工作, 規格衝突或範圍擴張先交回決策
完成後回報結果, 實際變更, checks 與未驗證範圍; 不執行未授權的 Git 歷史或遠端操作
```

## Read-only review

Reviewer 取得原始 requirements 與真實 diff; 不先要求證明某個方案正確 Finding 應描述 trigger 與影響, 無 finding 也是有效結果

```text
請 read-only review [revision / diff / artifact]
原始需求與驗收: [source pointers / acceptance criteria]
適用規則與範圍: [AGENTS.md / module / interface]
已知驗證: [實際 checks, 對應 revision 與限制]
要補足的風險: [具體 correctness / integration / safety 問題]

沿實際呼叫鏈核對相關實作, 區分 defect, unresolved question 與環境 blocker
每個 actionable finding 提供 file / Symbol, trigger, expected / actual, impact 與 evidence
不要為風格偏好要求無關 refactor; 不修改檔案或自行擴張實作範圍
回報 reviewed revision 與未覆蓋範圍; 沒有具體 finding 時明確說明
```

## Bounded worker

只在 subagent 授權與工具存在時使用; 交付完整迴圈, 而非每步需要 Main 指派的零碎操作 同一功能耦合的檔案與 checks 交給同一 owner

```text
你負責目前任務中的 [bounded 子交付], work ID: [ID]
僅擁有 [files / module / 行為] 的 discovery, edit, focused check 與 in-scope fix
你不是唯一正在工作的 owner; 保留其他人的變更並配合實際 concurrent state

目標與已確認做法: [outcome / decisions]
來源: [specification / source pointers / current version]
環境: [checkout / branch / starting revision / 必要未提交或 ignored 檔]
共享介面與相依: [已確認 properties / events / API 或 prerequisite]
Exclusions: [不可修改範圍]
驗收: [可獨立核對的 criteria]

在此邊界內自行完成 discovery, edit, check 與修復
規格衝突, 公共介面變更, 新架構決策, ownership 擴張或重複失敗時回報 Main, 並保留失敗證據
使用 [允許的 parent / subagent 管道] 接收更新, 回傳前確認納入有效決策
交付 changed behavior / files, checked revision / diff 或 hash, criteria 的 met / not met / unverified, 實際 checks, blockers 與 next action
回傳狀態是待驗收; Main 保留整合與最終接受責任
```

## 繼續或交接

在既有 progress record / chat context 保存有效狀態, 再提供必要引用; 不預設建立另一套紀錄 下列 prompt 本身不授權新 chat 或跨 chat 訊息

```text
請接續 [已授權交付], 目前 owner / work ID: [owner / ID]
目標與授權: [仍有效範圍]
Confirmed decisions / sources: [必要 source pointers 與版本]
環境: [repository / checkout / branch / HEAD / 相關未提交及 ignored 檔]
已完成且可沿用: [artifact / revision / 實際 checks 與限制]
尚未完成: [running / blocked / returned-pending-acceptance items, owners / IDs]
Pending updates: [尚待納入的使用者修正或來源變更]
失敗證據: [避免重做的嘗試與原因; 無則省略]
Ownership / dependencies: [先前 writer 狀態, 可修改範圍與前置條件]
驗收與下一步: [criteria / 下一個必要 action]

先對照目前來源與產物, 對帳 outstanding owners 後再開始依賴工作
保留已確認決策與 concurrent work; 新矛盾或範圍擴張交回 Main
更新既有 [獲授權 progress destination] 或目前 context, 不另建 backlog
如需對其他使用者 chat 傳訊, 先核對目的地 ID 與人類對該目的地的明確授權
```

## 如何縮短

來源已由 project guide 路由時只引用 guide; 沒有跨 owner 工作就省略同步與 ID 欄位 沒有失敗就省略嘗試紀錄; 不要為了填滿範本創造未確認的 facts

保留能改變實作或驗收結果的條件, 移除重複的全域偏好 如果目的仍不清楚, 增加可觀察的驗收情境比增加 model 指令更有用
