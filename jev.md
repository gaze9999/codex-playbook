# 何時使用 JEV

Jev 是 TypeSafe 提供的語意評估 model; 在這套流程中只協助已找到候選的閱讀排序或有限分類 Main 仍負責需求, 架構, ownership, 實作與驗收

操作來源維持於 [codex-setup Jev Skill](https://github.com/gaze9999/codex-setup/blob/main/skills/jev-evaluation/SKILL.md) 與 [操作教學](https://github.com/gaze9999/codex-setup/blob/main/docs/jev-usage.md); 這裡解釋選擇理由, 不複製 client, installer 或完整 API schema

## 先本地整理, 再判斷是否有價值

先用本機搜尋與 deterministic filters 核對 source identity / version, tracked state, dependencies 與必讀要求; 只有剩餘可選材料的語意順序或原子分類仍不清楚時才考慮 Jev

| 情境 | 合適做法 |
|---|---|
| 可選參考段落需要按目前問題安排閱讀順序 | 評估已獲准外傳的精簡候選, 保留全部 source pointers 在本地 |
| 多個摘要需要按明確且有限 criteria 分類 | 問單一語意條件, 保留 unknown, Main 核對原文與相依 |
| 檔案版本, ID, hash, counts, 日期或數字可直接比較 | 使用本機程式與確定性檢查 |
| 規格權威, permissions, API compatibility 或 acceptance 尚未確認 | Main 查驗來源與證據, 不交給分數決定 |
| 候選少, 順序已定或需要全面 review | 直接讀取與檢查; 不為展示工具而評分 |

沒有固定候選數量門檻, 不作為每輪 preflight, 不用來重選 Main / subagent / chat 路徑 日常入口仍是 Main, 使用者不必先決定是否使用 JEV

## 外傳與必讀內容

Jev inference 使用遠端 provider; query, rubric, candidates 與 summaries 都需要符合資料外傳授權 安裝或可呼叫工具不授權上傳公司 source, 私有規格, logs 或 customer data; 去識別化與摘要也不自動產生授權

必讀指示, governing specifications, acceptance criteria, confirmed decisions 與 blockers 保留在 Main; 排序只影響閱讀順序, 不改來源權威或 required verification

Rank helper 的 required entries 在本地保留, 不送其 text 評分; optional candidates 使用 opaque ID, ID 與檔案 / 行號 / 頁碼對照留在本地 每個 candidate 都保留, 不自動丟棄低分材料

## 問題與結果設計

問題只問一個明確的語意條件, instructions 與 criteria 對齊, 選項涵蓋不確定情況; 同一批必要 state 的獨立問題可合併, 不為 batch 放入無關全文

計數, 算術, 版本比較與 structural invariants 留給程式; 不要求 Jev 生成程式, 解釋或歷史摘要 這符合 provider 對 [Jev 1.13 failure modes](https://docs.typesafe.ai/model-jaggedness/jev-1.13) 的建議, 更換版本時仍需回查

Probability 與 confidence 不同: Choice / Score 的 confidence 反映答案機率分布的集中程度, Noul 沒有獨立 confidence; 它們都不是本專案事實正確率的證明 詳見 [TypeSafe confidence](https://docs.typesafe.ai/confidence)

採用 threshold 前, 用允許外傳且有預期答案的代表案例檢查正例, 反例與 unknown; 繁體中文與混合技術名稱另做驗證 [TypeSafe models](https://docs.typesafe.ai/models) 說明英文效果較佳, 其他語言需以自己的資料評估; alias 也可能指向不同版本, 依實際回應記錄 resolved model

## 能證明什麼

| 觀察 | 證明範圍 |
|---|---|
| 已安裝 / 註冊, local status 或離線 checks | 配置或本機通道, 未完成工作候選的遠端語意比較 |
| rank / evaluate 回傳 ok | 該次比較完成, 不代表 Main 接受或 application checks 通過 |
| fallback / skipped / dry-run | 依實際狀態未完成遠端比較, 回到既有流程 |

工具 unavailable, missing credential, malformed result 或判斷不可靠時, 保留原候選與 unknown, 由 Main 繼續處理; 不自動建立 reviewer, 新 chat 或額外 retry chain

實際使用後只簡短記錄用途, tool / status 與 Main 採用或 fallback 的方式, 回應有 model 才記錄 model; 不預設每輪 skip report, persistent logs 或監看

若使用者明確要求本機 metadata 監看, 依操作來源設定; 觀察統計不是 account total, remaining credits 或費用, 啟用記錄也不授權外傳內容

## 成本與採用判斷

Jev 的低 API 單價不能單獨證明整體工作省費; 比較時納入輸入整理, remote usage / latency, Main readback, correction 與 missed evidence

目前文件沒有宣稱 JEV 已改善此流程的總 token, latency 或品質; 測量原則見 [research.md](research.md) 只有實際有用且已授權的 bounded 問題才呼叫, 不因已安裝而增加工作
