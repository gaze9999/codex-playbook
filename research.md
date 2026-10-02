# 研究依據與採用理由

以下公開來源於 2026-10-02 核對; 日期代表文件閱讀時間, 不代表產品能力永遠不變 本文件記錄採用理由, 不宣稱這套流程已有品質, latency 或總成本 benchmark

## 官方能力與方法

| 來源 | 文件支持的範圍 | 此 playbook 的採用與限制 |
|---|---|---|
| [OpenAI AGENTS.md discovery](https://learn.chatgpt.com/docs/agent-configuration/agents-md) | Global 與 project 指示形成分層來源, 較接近工作目錄的指示可覆蓋較上層內容 | 將穩定偏好與 project 事實分開; 查驗目前 checkout 的有效指示, 不把 clone 當成 global 已安裝 |
| [OpenAI Subagents](https://learn.chatgpt.com/docs/agent-configuration/subagents) | 獨立工作可委派, 主對話收集結果; 寫入並行需要留意衝突與協調成本, model / effort 有設定與繼承規則 | 先看相依與 ownership, 不以 Main 的 model 決定 agent 數量; 有效設定仍需依當下 client 與 role 查驗 |
| [OpenAI Skills 與 prompt 指引](https://developers.openai.com/blog/rethinking-skills-and-prompts-for-gpt-6-astra) | Skill trigger 應明確, 詳細程序按條件載入; 常駐指示與過度細分步驟需要重新評估 | 常駐規則保持短, task 只保留本次目標與必要邊界; 此文章針對特定 model, 不推論所有 model 行為相同 |
| [Microsoft Test Impact Analysis](https://learn.microsoft.com/en-us/azure/devops/pipelines/test/test-impact-analysis?view=azure-devops) | 依修改相依選擇測試子集, 不能可靠判斷的情況需要較廣 fallback | 採用最小足夠且能檢驗改變行為的 checks; 不假設目前專案可直接使用該工具, 不取代必要 CI / release gate |

上述文件支持分層, bounded 工作與依相依選擇驗證的方向; 明確人類授權, 個人文件同步邊界與 returned / accepted 狀態是本 playbook 採用的治理規則, 不包裝成所有產品的固定要求

## 如何使用 community 經驗

本次也參考下列社群與作者來源作為候選方法, 不將單篇討論視為共識:

| 來源 | 採用方式與限制 |
|---|---|
| [r/codex: subagents without overusing](https://www.reddit.com/r/codex/comments/1ujjcxh/how_i_set_up_codex_subagents_without_overusing/) 與 [實際部署討論](https://www.reddit.com/r/codex/comments/1ujov69/how_do_you_actually_deploy_subagents_in_codex/) | 對照 bounded scope 與使用情境, 不從討論推論通用省費比例 |
| [r/ClaudeCode: where subagents pay off](https://www.reddit.com/r/ClaudeCode/comments/1ur70w0/where_do_subagents_actually_pay_off_in_typical/) 與 [是否使用 subagent](https://www.reddit.com/r/ClaudeCode/comments/1sr9c7k/to_subagent_or_not_to_subagent/) | 比較交接與 context 隔離的取捨; 不把另一產品的功能或設定直接搬到 Codex |
| [r/ClaudeAI: subagents and speed](https://www.reddit.com/r/ClaudeAI/comments/1u71d27/subagents_in_claude_code_arent_a_speed_trick/) | 提醒速度以外還有隔離價值, 仍需對實際工作量測 |
| [Peter Steinberger: Shipping at Inference-Speed](https://steipete.me/posts/2025/shipping-at-inference-speed) | 參考作者的直接工作與 context 管理經驗; 不採用未獲授權的自動提交或發布策略 |
| [obra/superpowers](https://github.com/obra/superpowers) | 參考明確子任務與 review 的設計, 不安裝或強制使用完整 pipeline |

X 來源曾嘗試 [Kaxil 的討論](https://x.com/kaxil/status/2037503513350005134) 與 [OpenAI Developers 的說明](https://x.com/OpenAIDevs/status/2033637455136731431), 但讀取受限; 不宣稱已核對其全文, 不用搜尋摘要支持技術結論. 持續追蹤可改查作者的原始文章與 repository, 並保留存取限制

社群案例可以提出候選 model 組合, prompt 或流程; 採用前回查官方能力, 自己的 source state, permissions 與 acceptance criteria

個人成功案例, 作者自述與某個 pipeline 的設定不等於社群共識; 不把它們當成目前 client 已 reload, 特定 model 支援 effort 或目前專案測試完整的證據

本 playbook 採用的是可驗收的 ownership 與必要 context 隔離, 沒有要求固定 planner / executor / reviewer tree 若案例沒有公開可重現的相同任務比較, 只記錄做法與 trade-off, 不引用為省費證明

## 要主張改善, 需要哪些證據

- 固定或記錄 source revision, environment, acceptance basis 與比較方式, 避免比較不同工作
- 計入完整 accepted result 的 input preparation, model usage, tools, retries, handoff, review, repair 與 elapsed time
- 記錄 missed requirements, defects, unverified items 與人工修正, 不只比較首次回應速度
- 使用代表性案例與反例; task, language, rubric 或 model version 改變時重新評估適用性

沒有上述量測時, 可以說明預期的 context 隔離或並行價值, 但不能宣稱低價 model, 較少檔案或多 agent 已降低總完成成本

## 維護研究紀錄

新增來源記錄連結, 閱讀日期, 支持範圍, 採用決策與限制; 將原始來源, 推論, 已確認決策與實際檢查分開

來源更新只修改受影響的解說與示例, 不要求每輪研究所有能力; 只有新採用 API, 新 model / effort, 新權限或存在疑義時才核對相關範圍

JEV 的 provider 來源, 校準與使用邊界另見 [jev.md](jev.md); 操作來源見 [codex-setup agents 說明](https://github.com/gaze9999/codex-setup/blob/main/agents/README.md), 安裝與 audit 仍由工具來源維護
