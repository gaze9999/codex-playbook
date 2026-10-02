# Codex Playbook 文件維護規則

- 本 repository 維護教學, 判斷理由與去識別化範例; 可執行 Skills, installers 與設定來源維持於 codex-setup, 不複製進來
- 修改前閱讀相關文件, links 與 Git status / diff, 保留其他人的變更; 只處理已授權文件範圍
- 使用繁體中文與台灣技術用語, 英文專有名詞保留; 使用半形英文標點與後接空白, 中文句尾不加句號
- Prompt 範例各自使用完整 `text` fenced code block, 保留 placeholders 與授權邊界; 不把所有欄位要求成每輪必填
- 只使用 generic 模組與示例資料; 不公開 company, project / transaction identifier, personal absolute path, chat ID, private endpoint, secret 或 transcripts
- 核對來源再描述工具與 configuration; 不捏造 model 支援, command, 安裝結果, runtime reload, benchmark 或 release 狀態
- Main 保留需求與架構決策, 直接實作, 整合與驗收; 文案不強制每輪委派或 reviewer chain
- 來源更新時同步受影響解說與連結, 將 proposal, confirmed decision 與實際 evidence 分開
- 驗證以 readback, relative link / fence / placeholder 檢查與 diff 為主; 不為文件工作安裝依賴或執行未授權 remote / Git history 操作
- 文件範例不授予 task creation, messaging, automation 或 publication 權限
- 以易理解為主; 流程與責任適合時用 Mermaid, 比較用表格, 需要操作才有助理解時用互動視覺化, 簡單內容保留文字; 圖中關係須與正文一致

- 本 repository 是持續維護的文件, 檢查後依授權 commit / push 至 main 即完成發布; 不例行升版本, 打 tag, 建立 GitHub Release 或封裝附件. 一般跨 repo 的 release 授權不套用到這裡, 除非使用者明確指定本 repo 的某次 release. 既有 tags / releases 僅為歷史紀錄
