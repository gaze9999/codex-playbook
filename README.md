# Codex Playbook

以可核對的來源, 清楚的 ownership 與實際驗收, 完成從需求到交付的 Codex 工作流程

這份 playbook 整理個人採用的治理原則與可重用範例, 適合自己換電腦時回查, 也適合團隊討論如何讓 agent 工作保持範圍清楚, context 連續與結果可驗證

[codex-setup](https://github.com/gaze9999/codex-setup) 維護可安裝的 global 指示, Custom Skills 與操作工具; 這裡維護教學, 判斷理由與示例 所有範例均經抽象化, 使用通用模組與 placeholder, 不包含實際專案或對話紀錄

## 來源與責任

| 來源 | 維護責任 |
|---|---|
| [my-py-tools](https://github.com/gaze9999/my-py-tools) | 獨立於 Codex 的通用 CLI / Python 工具與可重用 core |
| [codex-setup](https://github.com/gaze9999/codex-setup) | Codex Skills, agent 指示, configuration 與 adapter 安裝; 依版本使用通用 core, 不複製維護 core |
| codex-playbook | 可分享且去識別化的方法, 解說與範例 |
| 個人 Notion | 個人 context, 偏好, 學習筆記與未公開工作紀錄 |
| Project 文件 | 實際專案規格, 已確認決策, 進度與驗收證據 |

日常只有一個入口: 在 Main 說明目標與限制, 由 agent 依現況選擇工具, Skill 與 owner 使用者不必每次選擇所有層級或維護所有來源; 只有持久變更才更新受影響來源, 不要求每個任務同步五處, 多 agent 或 JEV

## 從哪裡開始

| 需求 | 閱讀入口 |
|---|---|
| 理解從需求到交付的完整流程 | [workflow.md](workflow.md) |
| 需要可複製並依任務刪減的 prompt | [prompts.md](prompts.md) |
| 換電腦, clone 後安裝或比對本機鏡像 | [portability.md](portability.md) |
| 分清常駐指示, Skill, 規格與進度紀錄 | [governance.md](governance.md) |
| 核對研究來源與採用理由 | [research.md](research.md) |
| 決定何時需要有限的語意評估 | [jev.md](jev.md) |
| 持續拓展知識並評估新技術 | [knowledge-radar.md](knowledge-radar.md) |
| 執行獨立安全檢查並保留證據 | [red-team.md](red-team.md) |
| 判斷新增 Skill 或抽出通用 Python 工具 | [toolkit-roadmap.md](toolkit-roadmap.md) |
| 讓 agent 維護這份文件 | [AGENTS.md](AGENTS.md) |

建議先讀 workflow, 再依目前問題選讀其餘文件; 不必每次任務都把整份 playbook 放入 context

## 工作原則

- Main 保留需求解讀, Architecture / Pattern 決策, context-heavy 工作, 必要直接實作, 整合與最終驗收
- 小型或高度相依的工作直接完成; bounded 且可獨立驗收的子工作, 才在授權與工具允許時委派
- Worker 擁有 discovery, edit, check 與 in-scope fix 完整迴圈, 交回可核對的結果與證據
- 需獨立維護且預期多輪執行的大型交付才考慮另外建立使用者 chat, 並取得明確授權
- 回傳待驗收與已驗收分開記錄; 使用者新決策必須傳到受影響 owner 並在驗收時確認納入
- 選擇最小且足夠的驗證, 保留必要的 CI / release gate, 如實揭露未驗證範圍

## 適用範圍與證據

本文件是可調整的工作方法, 不是每個任務都必須走過的固定 pipeline 不預設 planner / worker / reviewer 三段, 不依固定輪數或 context 長度分流, 也不把較小 model 視為較低總成本的證明

Codex 的可用 model, 工具, 權限與 configuration 規則可能改變; 使用前核對當下用戶端與官方文件 本 repository 沒有宣稱 agent latency, token 成本或跨平台 runtime 已通過 benchmark

文件範例不授予建立 chat, 傳送訊息, 安裝, 發布或變更外部服務的權限; 這些動作仍依當次使用者授權與實際環境規則處理

## 如何引用與維護

引用單一段落時, 同時保留它的條件與證據限制 將具體專案做法改成自己的模組名稱, 來源位置與驗收條件, 不直接複製成全域規則

操作工具的變更先回到 codex-setup; 教學的判斷理由與範例在這裡維護 來源更新後, 檢查受影響的解說, 連結與 prompt, 避免在兩個 repository 維護同一份 executable Skill

本 repository 以 main 分支的文件為目前版本; 文件檢查後 commit / push 即完成更新, 不另做版本號, tag, GitHub Release 或附件封裝. 需要固定引用時使用 commit permalink; 既有 tags / releases 僅為歷史紀錄. codex-setup 與 my-py-tools 的可安裝產物仍各自遵循版本與 release 流程
