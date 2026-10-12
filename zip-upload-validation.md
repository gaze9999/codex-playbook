# ZIP 上傳檢查範例

本文件說明兩種 ZIP 檢查方式, 保留結構檢查的判斷流程與小範例, 並提供只看副檔名及 MIME 的簡化版本. 範例使用通用名稱, 可依專案調整容量與訊息

## 先分清檢查範圍

| 方式 | 檢查資料 | 可以判斷的內容 |
|---|---|---|
| 副檔名與 MIME | `File.name`、`File.type` | 檔案名稱與瀏覽器提供的類型符合允許清單 |
| ZIP 結構檢查 | 檔案位元組、標頭、中央目錄與結尾記錄 | 指定支援範圍內的 ZIP 記錄位置與欄位一致 |
| 解壓與內容檢查 | 解壓結果、實際內容與資源消耗 | 檔案可解壓、內容符合業務規則 |

瀏覽器的 `File.type` 可能依副檔名與本機設定判定, 也可能是空字串, 無法單靠它證明內容是真正 ZIP. 以下簡化範例明確採取「副檔名與 MIME 都必須符合」的規則, MIME 空白時拒絕, 不自動接受 `application/octet-stream`. [MDN: Blob.type](https://developer.mozilla.org/en-US/docs/Web/API/Blob/type)

## ZIP 結構檢查流程

結構檢查會用 `file.arrayBuffer()` 讀取位元組, 再以 `DataView` 讀取 little-endian 整數. 主要流程如下:

1. 檢查最小長度, 依支援的 ZIP 變體核對起始記錄, 保留空 ZIP 的處理規則
2. 從尾端尋找 EOCD, 核對註解長度與檔案結尾
3. 讀取中央目錄位置、大小及項目數, 拒絕未支援的分卷格式
4. 遇到 ZIP64 標記時, 解析 locator、ZIP64 EOCD 與擴充欄位, 並檢查整數精度
5. 逐筆核對中央目錄記錄及可變長度欄位邊界
6. 依各筆 offset 找到 local header, 核對檔名、旗標、壓縮方式及資料範圍
7. 依 data descriptor 與標頭遮蔽旗標判斷大小/CRC 欄位是否可直接比對
8. 確認記錄完整走到中央目錄結尾

記錄格式與欄位定義依 [PKWARE ZIP APPNOTE](https://pkware.cachefly.net/webdocs/casestudies/APPNOTE.TXT), 結構一致只代表已檢查的記錄符合規則, 比對標頭 CRC 不等於對解壓內容重新計算 CRC

下列 TypeScript 範例只示範一般 EOCD 的定位, 可作為理解結構檢查的起點. 它沒有核對中央目錄、local header、ZIP64 或解壓內容, 不能當成完整 ZIP 驗證器

```typescript
function findEndOfCentralDirectory(buffer: ArrayBuffer): number {
  const view = new DataView(buffer);
  const recordSize = 22;
  if (view.byteLength < recordSize) return -1;

  const latest = view.byteLength - recordSize;
  const earliest = Math.max(0, latest - 0xffff);
  for (let offset = latest; offset >= earliest; offset--) {
    if (view.getUint32(offset, true) !== 0x06054b50) continue;
    const commentLength = view.getUint16(offset + 20, true);
    if (offset + recordSize + commentLength === view.byteLength) return offset;
  }
  return -1;
}
```

EOCD 的固定欄位占 22 bytes, 註解長度欄位占 2 bytes, 因此此範例最多往前找 65535 bytes 的註解範圍. 找到符合長度的候選記錄後仍需核對中央目錄, 註解內也可能出現相同簽章, 不能只因找到簽章就接受檔案

完整實作還需要界定支援的 ZIP 變體, 處理範圍錯誤與檔案讀取失敗. 空 ZIP 可以只有 EOCD, 不宜一律要求第一筆是 local header. 若只需要前端類型篩選, 可以採用下一節的簡化方式

## 簡化為副檔名與 MIME

`application/zip` 是登錄的 ZIP 類型, 範例另將 `application/x-zip-compressed` 納入相容清單, MIME 比對前去除前後空白並轉成小寫. [IANA: application/zip](https://www.iana.org/assignments/media-types/application/zip)

```typescript
function validateZipType(file: Pick<File, 'name' | 'type'>): string {
  const mime = file.type.trim().toLowerCase();
  return /\.zip$/i.test(file.name)
    && ['application/zip', 'application/x-zip-compressed'].includes(mime)
    ? '' : '請選擇 ZIP 檔案';
}

function validateZipSelection(files: ReadonlyArray<File>, maxBytes: number): string {
  if (files.length !== 1) return '請選擇一個檔案';
  const file = files[0];
  const typeError = validateZipType(file);
  if (typeError) return typeError;
  if (file.size > maxBytes) return '檔案超過容量限制';
  return '';
}
```

選取檔案的控制項可使用下列設定, 實際選取後仍呼叫上述檢查. `accept` 只提供檔案選擇提示, 不會完成類型驗證. [MDN: accept](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/accept)

```html
<label for="archive">選擇 ZIP 檔案</label>
<input id="archive" type="file"
       accept=".zip,application/zip,application/x-zip-compressed"
       aria-describedby="archive-error">
<p id="archive-error" role="status"></p>
```

以下選取流程只在檢查通過後換掉待上傳檔案, 拒絕選取或取消選取時保留上一個檔案

```typescript
const picker = document.querySelector<HTMLInputElement>('#archive')!;
const errorElement = document.querySelector<HTMLElement>('#archive-error')!;
let pendingFile: File | undefined;

picker.addEventListener('change', () => {
  const selected = Array.from(picker.files ?? []);
  picker.value = '';
  if (!selected.length) return;
  const error = validateZipSelection(selected, 10 * 1024 * 1024);
  errorElement.textContent = error;
  picker.setAttribute('aria-invalid', String(Boolean(error)));
  if (error) return;
  pendingFile = selected[0];
});
```

範例的容量上限是壓縮檔本身的 `File.size`, 不包含解壓後總大小、項目數或壓縮比. 上傳端仍需依業務規則檢查實際內容, 有解壓流程時另限制資源消耗與輸出路徑, 前端名稱與 MIME 篩選不能替代這些檢查

簡化類型檢查時仍需保留專案既有的單檔數量、有效附件合計容量、唯讀限制、資料切換保護及保存方式. 若原呼叫端已使用非同步函式, 可先保留其 Promise 介面, 不必為改掉位元組解析同步重整所有呼叫端

## 驗收範例

| 檔名 / MIME / 操作 | 簡化版本預期 |
|---|---|
| `report.zip` / `application/zip` | 通過類型檢查 |
| `REPORT.ZIP` / `application/x-zip-compressed` | 通過類型檢查 |
| `report.zip` / ` APPLICATION/ZIP ` | 正規化後通過類型檢查 |
| `report.zip` / 空字串 | 拒絕, 保留上一個待上傳檔案 |
| `report.zip` / `text/plain` 或 `application/octet-stream` | 拒絕, 保留上一個待上傳檔案 |
| `report.txt` / `application/zip` | 拒絕, 保留上一個待上傳檔案 |
| 兩個檔案 | 依單檔規則拒絕 |
| 一個類型符合的檔案 / 超過容量限制 | 拒絕, 保留上一個待上傳檔案 |
| 一個類型符合的檔案 / 剛好等於容量上限 | 通過範例的容量檢查 |
| `report.zip` / `application/zip` / 0 bytes | 通過前端類型與容量檢查, 空檔是否可上傳另依業務規則 |
| 取消選取 | 保留上一個待上傳檔案 |
| 任意內容, 但檔名/MIME 皆符合 | 通過前端類型檢查, 內容真偽不在此檢查範圍 |

自動檢查可使用 `new File(['sample'], 'report.zip', { type: 'application/zip' })`, 並令測試檔案的 `arrayBuffer()` 拋出錯誤, 確認簡化檢查完全不讀取內容. 瀏覽器驗收另外操作有效選取、拒絕選取、取消與換檔, 核對畫面訊息與保留的檔名

回到 [Playbook 首頁](README.md)
