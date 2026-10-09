# 研究參考與教學依據

這份文件保留原始來源, 採用理由與適用範圍, 可用來準備教學, 比較工作方法或追查一項決策

第一節的官方文件, Jev 來源與兩篇標示回查的實務文章於 2026-10-05 閱讀, 日期代表查閱時間, 延伸閱讀保留先前的 2026-10-02 紀錄

## 官方能力與採用理由

| 來源 | 支持的內容 | 教學中的用法 |
|---|---|---|
| [OpenAI AGENTS.md](https://learn.chatgpt.com/docs/agent-configuration/agents-md) | Global 與專案指示的查找順序, override 與工作目錄分層 | 用圖或目錄例子解釋規則放哪裡, 操作時確認實際載入來源 |
| [OpenAI 個人化設定](https://learn.chatgpt.com/docs/personalize) | 自訂指示, Work 網頁寫作風格與記憶設定 | 將帳戶偏好與本機規則分開操作 |
| [OpenAI Developer settings](https://learn.chatgpt.com/docs/developer-settings) | 本機用戶端的設定與 MCP 連接, 雲端 Work 的設定來源 | 安裝本機工具後另確認目標用戶端, 帳戶連接在其介面授權 |
| [OpenAI Memories](https://learn.chatgpt.com/docs/customization/memories) | 雲端與本機記憶的不同來源與管理方式 | 必守規則保存在指示, 記憶用來回查 |
| [OpenAI Projects](https://learn.chatgpt.com/docs/projects) | Project 的指示, 檔案與來源, 本機工作目錄的使用方式 | 新人先分清 ChatGPT Project 與本機專案 |
| [OpenAI Subagents](https://learn.chatgpt.com/docs/agent-configuration/subagents) | 子工作分工, 結果彙整與平行寫入的協調 | 先教單 agent 完成流程, 再練習可獨立驗收的分工 |
| [Microsoft Test Impact Analysis](https://learn.microsoft.com/en-us/azure/devops/pipelines/test/test-impact-analysis?view=azure-devops) | 依程式碼與測試的相依關係選擇受影響測試 | 用來說明按變更選測試, 該工具的支援範圍另依文件核對 |
| [Git gitignore](https://git-scm.com/docs/gitignore) | 忽略未追蹤檔案, 已追蹤檔需先從 index 移除 | 說明本機指示檔, 備份與公開文件如何分開管理 |
| [textlint MCP](https://textlint.org/docs/mcp/) | 使用已設定的規則檢查文字或檔案 | 先準備詞表與標點規則, 修正後再跑檢查 |

Test Impact Analysis 的文件列有 Visual Studio Test 與 .NET Framework 等支援條件, 教學採用的是依相依選擇測試的方法, 前端或其他語言使用各專案的測試工具

## 人類實務討論

官方文件用來確認產品行為, 作者與社群案例用來觀察實際做法, 下表標明此次回查與先前閱讀紀錄

| 來源 | 查閱紀錄 | 可帶入教學的問題 |
|---|---|---|
| [r/codex: How I set up Codex subagents without overusing them](https://www.reddit.com/r/codex/comments/1ujjcxh/how_i_set_up_codex_subagents_without_overusing/) | 2026-10-05 回查, 個人使用自述 | 子工作怎麼定範圍, 為什麼小工作直接做, 如何在穩定的版本上審查 |
| [Peter Steinberger: Shipping at Inference-Speed](https://steipete.me/posts/2025/shipping-at-inference-speed) | 2026-10-05 回查, 作者工作經驗 | 如何用短需求與畫面反覆調整, 將重要功能知識保存在專案文件 |
| [r/codex: 實際部署 subagent](https://www.reddit.com/r/codex/comments/1ujov69/how_do_you_actually_deploy_subagents_in_codex/) | 2026-10-02 閱讀紀錄 | 探討分工的使用情境與交接成本 |
| [r/ClaudeCode: Where do subagents pay off](https://www.reddit.com/r/ClaudeCode/comments/1ur70w0/where_do_subagents_actually_pay_off_in_typical/) | 2026-10-02 閱讀紀錄 | 比較閱讀隔離與跨工作協調 |
| [r/ClaudeCode: To subagent or not](https://www.reddit.com/r/ClaudeCode/comments/1sr9c7k/to_subagent_or_not_to_subagent/) | 2026-10-02 閱讀紀錄 | 哪些工作值得拆分, 哪些直接完成 |
| [r/ClaudeAI: Subagents and speed](https://www.reddit.com/r/ClaudeAI/comments/1u71d27/subagents_in_claude_code_arent_a_speed_trick/) | 2026-10-02 閱讀紀錄 | 分開評估速度與 Context 隔離的價值 |
| [obra/superpowers](https://github.com/obra/superpowers) | 2026-10-02 閱讀紀錄 | 觀察子任務與審查的流程設計 |
| [OpenAI Skills 與 prompt 指引](https://developers.openai.com/blog/rethinking-skills-and-prompts-for-gpt-6-astra) | 2026-10-02 閱讀紀錄, 特定 model 的官方建議 | 檢視 Skill 的使用時機與常駐指示長度 |

社群貼文中的 model, effort 與設定屬於作者當時環境, 教學使用其工作問題與分工方法, 實作時回到官方文件及目前專案確認

## 遊戲開發與數值研究

2026-10-05 查閱 Machinations, 科學計算, 公式與 property-based testing 的官方文件, 並閱讀近期放置遊戲開發者討論, 工作方法與範例見 [game-balance.md](game-balance.md), 以下保留原始來源與採用理由, 相依與安裝流程由工具來源維護

起手方式為共用正式規則的模擬器, 試算表與專案測試, 保留不同策略, 未達成目標的路徑與試玩, 不從單一平均或參數搜尋結果判斷遊戲體驗

以下於 2026-10-05 查閱, 官方文件支持工具能力, 社群自述用來理解實際工作方式

| 來源 | 支持的內容 | 採用方式 |
|---|---|---|
| [NumPy random](https://numpy.org/doc/stable/reference/random/index.html) | Generator 與抽樣介面 | 固定 RNG 實作與輸入, 比較隨機路徑 |
| [SciPy differential evolution](https://docs.scipy.org/doc/scipy/reference/generated/scipy.optimize.differential_evolution.html), [bootstrap](https://docs.scipy.org/doc/scipy/reference/generated/scipy.stats.bootstrap.html) | 搜尋與重抽樣統計 | 候選參數搜尋, 另保留驗證情境與不確定性 |
| [SymPy lambdify](https://docs.sympy.org/latest/modules/utilities/lambdify.html) | 符號運算式與數值計算的銜接 | 先推導再對照實際核心, 輸入為已核對的模型 |
| [fast-check model-based testing](https://fast-check.dev/docs/advanced/model-based-testing/) | 操作序列, 縮減與重播參數 | 保留完整的失敗重播資料 |
| [Hypothesis stateful tests](https://hypothesis.readthedocs.io/en/latest/stateful.html) | 規則與狀態機測試 | Python 模型使用實際狀態不變量 |
| [Machinations 文件](https://machinations.io/docs), [方案](https://machinations.io/pricing) | 資源流模型與模型公開範圍 | 複雜循環需要時選用, 不公開私有設計 |
| [Wolfram MCP](https://www.wolfram.com/artificial-intelligence/mcp/) | Local 與 Cloud 的計算接法 | 沿用既有設定並依執行範圍選用 |
| [SimPy](https://simpy.readthedocs.io/en/latest/), [Optuna](https://optuna.readthedocs.io/en/stable/) | 離散事件與參數最佳化 | 有排隊或大量參數搜尋需求後再加入 |
| [r/incremental_gamedev: How do you balance your numbers?](https://www.reddit.com/r/incremental_gamedev/comments/1utq0na/how_do_you_balance_your_numbers/) | 使用者分享試算表, 共用核心的 headless 模擬與試玩, 也有人提醒模型可能耗掉開發時間 | 先量測重要選擇之間的時間, 小範圍調整, 保留試玩 |
| [fast-check 使用者與維護者討論](https://github.com/dubzzz/fast-check/discussions/6166) | Model-based 失敗重播的實際問題 | 對照官方 replay 說明, 不把個人做法當成保證 |

## Jev 的資料來源

| 來源 | 支持的內容 | 採用方式 |
|---|---|---|
| [TypeSafe Models](https://docs.typesafe.ai/models) | model alias, 實際 model ID 與語言支援 | 保存回應版本, 繁中與混合語言用代表案例評估 |
| [TypeSafe Confidence](https://docs.typesafe.ai/confidence) | Choice / Score 的 confidence 與 Noul 機率 | 理解回應欄位, 再用自己的案例校準門檻 |
| [Jev 1.13 已知失敗情境](https://docs.typesafe.ai/model-jaggedness/jev-1.13) | 數值, 日期, 無關資料與複雜間接問題的限制 | 本機先整理資料, 精確比較交給程式 |

工作中的使用時機與結果判讀見 [jev.md](jev.md), 設定與 API 參數依所用介面的實際版本核對

## 想比較改善效果, 要記錄什麼

| 項目 | 記錄方式 |
|---|---|
| 比較基礎 | 同一需求, 來源版本, 環境與驗收條件 |
| 完整工作量 | 輸入整理, model 與工具用量, 重試, 交接, 審查與修正 |
| 時間 | 從開始到結果被驗收的總時間 |
| 品質 | 漏掉的需求, 問題, 未驗證範圍與人工修正 |
| 適用性 | 代表案例, 反例, 語言與 model 版本 |

先說明設計理由, 有比較結果後再說改善幅度, 工具的輸出壓縮率與 API 單價分別記錄, 總成本依完整工作量計算

## 新人教學建議

1. 用一個小功能練習需求, 閱讀, 修改與驗收
2. 將共用偏好, 專案規格與當次進度放到正確位置
3. 安裝一個需要的工具, 完成連接與代表性呼叫
4. 練習一個有明確介面與完成條件的子工作
5. 對照單人與分工結果, 討論交接成本與實際收益

每次示範保留來源, 操作與結果, 公開教材使用虛構資料, 學員可依自己的專案替換例子

## 維護研究紀錄

新增來源記錄連結, 查閱日期, 支持的內容與採用理由, 將原始資料, 推論及實際驗證分開

來源或能力改變時更新受影響教學, 未重新閱讀的來源保留原查閱日期, 無法取得原文的候選列為待核對
