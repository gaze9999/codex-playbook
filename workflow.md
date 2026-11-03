# 從需求到驗收

## 開發時怎麼自我檢驗

1. 開工前從規格寫出可觀察的預期結果, 例如輸入無效時必須拒絕寫入, 選一個可重跑的入口
2. 修缺陷時先重現舊行為, 留下失敗原因, 修正後用相同輸入重跑, 補一個應維持原行為的相鄰案例
3. 檢查實際結果, 涉及瀏覽器就操作使用者會用的入口, 涉及儲存就重新開啟並讀回, 涉及安裝就從目標用戶端呼叫一次
4. 交付時並列預期、實際結果與未驗範圍, 跨工具接手時沿用同一份測資與來源版本, 對預期有爭議就回查規格

[Playwright 官方測試原則](https://playwright.dev/docs/best-practices) · [Anthropic 的代理評估方法](https://www.anthropic.com/research/demystifying-evals-for-ai-agents) · [Simon Willison 的紅綠測試實務](https://simonwillison.net/guides/agentic-engineering-patterns/red-green-tdd/)
