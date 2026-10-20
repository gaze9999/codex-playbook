# 研究參考與教學依據

這份文件保留原始來源, 採用理由與適用範圍, 可用來準備教學, 比較工作方法或追查一項決策

第一節的官方文件, Jev 來源與兩篇標示回查的實務文章於 2026-10-05 閱讀, 日期代表查閱時間, 延伸閱讀保留先前的 2026-10-02 紀錄, 後續回查日期另標於相關主題

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
| [Firecrawl 連線方式](https://docs.firecrawl.dev/mcp-server)與 [keyless MCP](https://docs.firecrawl.dev/mcp-server/keyless) | 2026-10-17 查核, 支援原生 connector、OAuth 或 API key, keyless 僅提供受限工具, 工具範圍依實際連線及方案核對 | 將已認證 App 納入公開網頁查找選項, 分開確認其他 MCP 的認證、team 與額度, 安裝不代表成功呼叫, 換入口不推定免費 |
| [OpenAI approvals and security](https://learn.chatgpt.com/docs/agent-approvals-security) | 2026-10-21 核對, command sandbox、approval、網路授權與 proxy 分開, 命令網路不涵蓋所有工具管道 | 先辨識本機 / 雲端與 shell / App / MCP / 瀏覽器, 不由單一結果推論全部路徑或自行放寬權限 |
| [OpenAI 評估實務](https://developers.openai.com/api/docs/guides/evaluation-best-practices#llm-as-a-judge-and-model-graders) | 2026-10-21 核對, Judge 可能受順序及篇幅影響, 需對照人工標記 | 獲准比較時加入換序與篇幅對照, 分列錯誤放行、人工一致及總成本, 不以分數取代可執行驗收, 尚未進行模型試驗 |
| [openpyxl 公式](https://openpyxl.readthedocs.io/en/stable/simple_formulae.html)及 [XlsxWriter 結果](https://xlsxwriter.readthedocs.io/working_with_formulas.html) | 2026-10-21 核對, 寫公式、快取值與目的 client 實際重算分開 | 文件需要計算結果時另核對重算、引用與必要物件保留, 未做文件實測 |
| [Storybook a11y](https://storybook.js.org/docs/writing-tests/accessibility-testing) | 2026-10-21 核對, todo 不產生 CI 的 a11y 輸出或失敗, error 才因違規失敗 | 僅在已有相容 Storybook 的專案核對實際模式、版本及 story / 狀態範圍, 未做產品驗證 |
| [textlint MCP](https://textlint.org/docs/mcp/) | 使用已設定的規則檢查文字或檔案 | 先準備詞表與標點規則, 修正後再跑檢查 |

Test Impact Analysis 的文件列有 Visual Studio Test 與 .NET Framework 等支援條件, 教學採用的是依相依選擇測試的方法, 前端或其他語言使用各專案的測試工具

## 持久流程與指示效果

以下於 2026-10-13 依跨專案接續與流程設計的缺口回查, 採用範圍見 [可持續的 AI 開發流程](ai-workflow.md), 論文閱讀限方法、結果與限制的相關段落, 不宣稱已重現實驗

| 來源與證據類型 | 可用結論 | 採用限制 |
|---|---|---|
| [OpenAI Remote handoff](https://learn.chatgpt.com/docs/remote-connections#hand-off-a-chat-between-hosts), 官方產品文件 | 目的主機需有相符專案與 repository 子目錄, 轉移聊天及 Git 狀態 | 不支援轉到 Codex cloud, 目的裝置內容與環境仍需核對 |
| [OpenAI Dots tasks and memory](https://learn.chatgpt.com/docs/dots/tasks-and-memory), 官方產品文件 | 記憶、task 對話、執行環境與排程用途不同 | 改選電腦不搬移既有 task, 完成一次執行仍需成果驗收 |
| [Evaluating AGENTS.md v3](https://arxiv.org/html/2602.11988v3), 2026-09-29 修訂的預印本 | 在其程式修復基準比較有無 repository context, 未普遍提高完成率, 建議評估實際效益 | 受測模型、任務與成功指標有限, 不據此移除必要授權、安全或專案規則 |
| [SkillsBench v4](https://arxiv.org/html/2602.12670v4), 2026-06-14 修訂的預印本 | 用配對任務比較有無 curated Skills, 結果隨任務及 model/harness 而異 | 任務內 Skill 組合不是安裝總量上限, 不把平均提升套用到目前環境 |
| [Peter Steinberger 的工作經驗](https://steipete.me/posts/2025/shipping-at-inference-speed), 作者實務自述 | 以可操作成果反覆調整, 按功能保存文件, 視相依使用既有專案方法 | 個人工作方式與舊模型環境, 不採用其自述倍數作成效證據 |
| [r/codex 原討論與回覆](https://www.reddit.com/r/codex/comments/1w1j1qi/could_an_agentsmd_file_actually_reduce_codex/), 社群意見 | 有人支持精簡與索引, 也有人指出模糊省費指示增加判斷負擔 | 沒有共同受控任務, 不推論節省比例或社群共識 |

採用的設計是保留必要限制、把細節放條件式入口、用代表任務驗收, 比較時記錄實際 model/client、來源版本、載入內容、環境、返工、結果與可取得的總成本, 分開標示人工檢視、確定性檢查與模型實測

## 近期相依研究與不同實務的比較

以下於 2026-10-13 從分工、長流程、壓縮與記憶的設計問題擴大查找, 包含近期原始論文及其引用的相依方法, 不以新舊或引用數決定權威, 論文閱讀涵蓋下列判斷所需的方法、結果與限制段落, 沒有重現實驗, 作者文章與討論的閱讀範圍另列

| 原始來源、版本與類型 | 本次讀到的證據與限制 | 對流程的採用判斷 |
|---|---|---|
| [Towards a Science of Scaling Agent Systems v3](https://arxiv.org/html/2512.08296v3), 預印本, 2026-04-08 修訂 | 六個基準、260 組設定, 修訂後對部分協調成本與錯誤傳播關係降低確定性, 較穩定的是原有能力與增益飽和的關係 | 分工按任務相依及實際成本評估, 不引用早期文章的效果值當現行定律, 修訂要回查已採用結論 |
| [When Agents Coordinate v1](https://arxiv.org/html/2608.16801v1), 預印本, 2026-08-17 | 兩個合成 Python 任務、單一 runtime/model, 包含封閉評分的後續驗證, 協調方法依工作型態有不同成本, 指定 coordinator 名稱未可靠改善結果 | 明定檔案、介面與實際 owner, 不把固定角色名稱或 Agent 數量當成效保證 |
| [The Compaction Cliff v1](https://arxiv.org/html/2608.22752v1), arXiv 版本, 2026-08-24 | 比較不同保留策略, 分類器召回不等於執行遵守率, 公開資料與部分重建基準有外推限制, 部分行為比較未匹配 token 量 | 精確限制、授權與文案保留原文或可查核來源, 壓縮後驗收相關行為, 不引用其比例描述 Codex 的遺漏率 |
| [Just-in-Time Memory v1](https://arxiv.org/html/2609.27334v1), 預印本, 2026-09-23 | 在 ALFWorld、WebShop、tau2 比較讀取時整理與既定記憶, 使用受訓 curator、固定檢索方式與 benchmark 格式, 額外呼叫有成本 | 依目前任務整理獲准來源, 與寫入時摘要互補, 不因此全量保存私人對話或宣稱現有產品具有同一機制 |
| [MemHarness v1](https://arxiv.org/html/2607.28272v1), 預印本, 2026-07-30 | 在 ALFWorld、WebShop 以 Qwen2.5-7B、受訓策略及檢索原則進行狀態相關的重建, 本次讀取方法與實驗設定 | 找到相似經驗後仍核對現在的狀態與限制, 不能直接重播舊操作, 不把受訓模型結果外推到一般提示詞 |
| [SkillOS v1](https://arxiv.org/html/2605.06614v1), 預印本, 2026-05-07 | 在相依任務序列訓練 Skill curator, executor 固定, 使用簡單檢索與扁平 Markdown Skill, 不涵蓋腳本、支援資源及階層 Skill | 候選方法用後續代表案例驗收, 不據此自動改寫偏好、增加 Skills 或推定多檔 Plugin 的效果 |
| [METR 開發實驗更新](https://metr.org/blog/2026-02-24-uplift-update/), 原研究團隊報告, 2026-02-24 | 閱讀正文與方法變動, 後續實驗受到是否接受無 AI 工作、任務選擇、報酬與時間估計偏差影響, 作者不支持強的當期效果估計 | 舊實驗的減速結論不能當今天的普遍結果, 比較須保留選樣、工作內容與完整驗收成本 |
| [METR 使用調查](https://metr.org/blog/2026-05-11-ai-usage-survey/), 調查報告, 2026-05-11 | 閱讀摘要與相關方法說明, 區分自述工作價值與速度, 作者對自述改善幅度保持保留, 不是隨機對照結果 | 分開記錄交付價值與時間, 不將自評倍數換算成自己的生產力 |
| [Mitchell Hashimoto 的採用歷程](https://mitchellh.com/writing/my-ai-adoption-journey), 作者實務自述, 2026-02-05 | 閱讀全文, 用熟悉任務比較成果、改善可驗證環境與重複失敗, 作者也保留自己的工作偏好 | 用已知任務建立基準, 重複問題修正正確來源, 不把作者的常駐工作習慣當持續執行授權 |
| [Simon Willison: Subagents](https://simonwillison.net/guides/agentic-engineering-patterns/subagents/), 作者指南 | 閱讀本章正文, 強調隔離 Context 與獨立工作, 未取得本章明確發布日期, 查閱日為 2026-10-13 | 按閱讀隔離與驗收負擔決定分工, 主 Agent 有足夠脈絡時可以直接檢查, 不要求固定審查鏈 |
| [Anthropic 長流程 harness 設計](https://www.anthropic.com/engineering/harness-design-long-running-apps), 廠商工程案例, 2026-03-24 | 閱讀架構、驗收與模型更新段落, 新模型後移除部分流程, 單人與完整流程產物範圍不同, 時間/費用不能直接比較效率 | 改模型後一次評估一個流程元件, 用代表成果決定保留或簡化, 不固定套三 Agent 或自動擴充產品範圍 |
| [r/codex 壓縮退步討論](https://www.reddit.com/r/codex/comments/1wxzsma/major_compaction_regression/), 社群原文及回覆 | 2026-10-13 閱讀, 搜尋日期與頁面相對時間不一致, 反映遺忘更正與重做已完成工作, 無官方根因或修正驗證 | 將最新更正、已完成項目與未完工作納入恢復案例, 不採用留言設定作已證實解法 |
| [r/codex Manage lowusage guide](https://www.reddit.com/r/codex/comments/1vshn7e/manage_low_usage_guide/), 社群原文 | 2026-10-13 閱讀原文, 未取得可讀回覆, 日期顯示不一致, 倡議少重查且反對分工, 節省幅度未受控驗證 | 保留避免重跑無關檢查的問題意識, 不採用一律禁用 Agent、固定模型或節省比例 |

這些來源支持的是有條件的設計選擇: 寫入時保存精確決策, 讀取時按任務重建所需脈絡, 再以實際行為驗收, 它們不是互斥的記憶產品方案, 也不能省掉來源權威、資料權限與目的端驗證

時效性要追到採用位置, 例如 Scaling Agent Systems 的 v3 修訂會使早期效果值及確定性需要重查, 不只是刷新查閱日期, 一篇新記憶論文則先形成待評估候選, 不直接取代既有工作規範, 具體管理方式見 [來源變更與採用影響](ai-workflow.md#來源變更與採用影響)

## 人類實務討論

官方文件用來確認產品行為, 作者與社群案例用來觀察實際做法, 下表標明此次回查與先前閱讀紀錄

| 來源 | 查閱紀錄 | 可帶入教學的問題 |
|---|---|---|
| [r/codex: How I set up Codex subagents without overusing them](https://www.reddit.com/r/codex/comments/1ujjcxh/how_i_set_up_codex_subagents_without_overusing/) | 2026-10-05 回查, 個人使用自述 | 子工作怎麼定範圍, 為什麼小工作直接做, 如何在穩定的版本上審查 |
| [Peter Steinberger: Shipping at Inference-Speed](https://steipete.me/posts/2025/shipping-at-inference-speed) | 2026-10-12 回查, 作者工作經驗 | 如何用短需求與畫面反覆調整, 將重要功能知識保存在專案文件 |
| [r/codex: 實際部署 subagent](https://www.reddit.com/r/codex/comments/1ujov69/how_do_you_actually_deploy_subagents_in_codex/) | 2026-10-02 閱讀紀錄 | 探討分工的使用情境與交接成本 |
| [r/ClaudeCode: Where do subagents pay off](https://www.reddit.com/r/ClaudeCode/comments/1ur70w0/where_do_subagents_actually_pay_off_in_typical/) | 2026-10-02 閱讀紀錄 | 比較閱讀隔離與跨工作協調 |
| [r/ClaudeCode: To subagent or not](https://www.reddit.com/r/ClaudeCode/comments/1sr9c7k/to_subagent_or_not_to_subagent/) | 2026-10-02 閱讀紀錄 | 哪些工作值得拆分, 哪些直接完成 |
| [r/ClaudeAI: Subagents and speed](https://www.reddit.com/r/ClaudeAI/comments/1u71d27/subagents_in_claude_code_arent_a_speed_trick/) | 2026-10-02 閱讀紀錄 | 分開評估速度與 Context 隔離的價值 |
| [obra/superpowers](https://github.com/obra/superpowers) | 2026-10-02 閱讀紀錄 | 觀察子任務與審查的流程設計 |
| [OpenAI Skills 與 prompt 指引](https://developers.openai.com/blog/rethinking-skills-and-prompts-for-gpt-6-astra) | 2026-10-02 閱讀紀錄, 特定 model 的官方建議 | 檢視 Skill 的使用時機與常駐指示長度 |

社群貼文中的 model, effort 與設定屬於作者當時環境, 教學使用其工作問題與分工方法, 實作時回到官方文件及目前專案確認

## 中途訊息、載入與檔案檢查

以下來源於 2026-10-12 查閱, 分別支持 [中途修正](workflow.md#8-納入中途修正)、[載入核對](portability.md#確認目前對話是否已載入) 與 [ZIP 上傳檢查](zip-upload-validation.md)

| 來源 | 支持的內容 | 採用方式 |
|---|---|---|
| [OpenAI Steer / Queue](https://learn.chatgpt.com/docs/prompting#steering-and-queuing) | Steer 加入目前執行, Queue 留到下一次執行 | 將訊息送達方式與工作範圍判斷分開 |
| [OpenAI Skills](https://learn.chatgpt.com/docs/build-skills) | Skill 探索與按需載入 | 分開確認可用清單、安裝內容與本次讀取 |
| [MDN Blob.type](https://developer.mozilla.org/en-US/docs/Web/API/Blob/type) | 類型可能依副檔名判定, 也可能為空字串 | 名稱與 MIME 僅作前端篩選, 明定空 MIME 的處理 |
| [MDN accept](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/accept) | 檔案選擇提示不執行類型驗證 | 選取後仍檢查, 上傳端另核對要求 |
| [IANA application/zip](https://www.iana.org/assignments/media-types/application/zip) | 登錄的 ZIP MIME 名稱 | 使用 application/zip, 額外相容類型由範例清單明定 |
| [PKWARE ZIP APPNOTE](https://pkware.cachefly.net/webdocs/casestudies/APPNOTE.TXT) | EOCD、ZIP64、中央目錄與 local header 欄位, 空 ZIP 的規則 | 示範記錄定位並標出未涵蓋的完整驗證 |

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
