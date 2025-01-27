# Web Data Scraper (ttkbootstrap)

這是一個以 **Python**、**Selenium**、**BeautifulSoup** 為基礎，並結合 **ttkbootstrap** 的 GUI 專案，提供使用者在圖形介面上輸入/選擇目標網址和 CSS 選擇器，然後擷取網頁中的資料並預覽、刪除欄位，最後可匯出成 CSV 檔案。

---

## 目錄
1. [功能特色](#功能特色)
2. [環境需求](#環境需求)
3. [安裝與使用步驟](#安裝與使用步驟)
4. [常見問題 (FAQ)](#常見問題-faq)
5. [授權](#授權)

---

## 功能特色
1. **圖形介面 (GUI)**  
   透過 `ttkbootstrap` 提供更美觀的介面風格。
2. **多執行緒處理**  
   當程式進行網頁抓取或刪除欄位等耗時操作時，不會凍結畫面，提供更順暢的使用者體驗。
3. **自訂 CSS 選擇器**  
   使用者可輸入或選擇預設的 Selector，針對不同網頁結構動態調整，抓取更彈性。
4. **資料預覽與欄位刪除**  
   先顯示前5筆資料，讓使用者可以快速刪除不需要的欄位。
5. **完整資料查看**  
   可在 Treeview 中查看完整擷取資料，並支援 `Ctrl + C` 或 `Command + C` 複製貼上至 Excel。
6. **匯出 CSV**  
   一鍵匯出擷取結果，並採用 `UTF-8-SIG` 編碼，方便跨平台閱讀。

---

## 環境需求
- **Python 3.7+**  
- **Google Chrome** (或相容的 Chromium 瀏覽器)  
- 對應版本的 **ChromeDriver**  
- 以下 Python 套件：
  - `selenium`
  - `bs4` (BeautifulSoup)
  - `pandas`
  - `ttkbootstrap`

---

## 安裝與使用步驟

1. **下載/克隆此專案**  
   - 直接在 GitHub 上下載 Zip，或使用下列指令克隆：
     ```bash
     git clone https://github.com/<YourUserName>/<YourRepository>.git
     ```
   - 進入專案資料夾：
     ```bash
     cd <YourRepository>
     ```

2. **安裝所需套件**  
   在命令提示字元或終端機輸入：
   ```bash
   pip install -r requirements.txt
   ```

3. 若尚未建立 requirements.txt，請自行建立，內容包含：
　- selenium
　- beautifulsoup4
　- pandas
　- ttkbootstrap

4. 設定 ChromeDriver

- 下載與你 Chrome 版本相符的 chromedriver (可至 ChromeDriver 官方網站)。
- 將 chromedriver.exe 放至電腦中任一路徑，並於程式中 CHROME_DRIVER_PATH 修改為你的絕對路徑：

```python=
CHROME_DRIVER_PATH = r"C:\Users\user\Downloads\chromedriver-win64\chromedriver.exe"
```

5. 執行程式
- 在專案資料夾下執行：
```bash=
python web_data_scraper.py
```
順利的話，應會彈出一個 ttkbootstrap 風格的 GUI 視窗。




6. 使用操作說明
   1. 選擇或輸入網址：
    - 預設值有 https://www.costco.com.tw/ 和 https://24h.pchome.com.tw/，也可自行輸入其他網址。
    - ![image](https://hackmd.io/_uploads/BJ2jg7Sukl.png)

   2. CSS Selector (選填)：

    - 預設提供常見的選擇器，如 .product-item、.prod_container 等，也可自行輸入。
    - 若留空，程式會抓整個網頁的所有標籤。
    3. 點擊「擷取資料」：
    - 程式會以 Selenium 自動開啟瀏覽器，抓取頁面內容並使用 BeautifulSoup 分析。
    - 約等待數秒(或依網頁複雜度調整程式中的 time.sleep)，即可於視窗中看到前5筆擷取結果。
    - ![07](https://hackmd.io/_uploads/BkkN-mr_1x.jpg)
    4. 刪除不要的欄位：
    - 每個欄位上方會有「X」按鈕。點選後，即可刪除該欄位。
    - ![08](https://hackmd.io/_uploads/rkbvZQSOJl.jpg)
    5. 「顯示完整資料」：
    - 點擊後會顯示所有擷取之資料，並可用 Ctrl + C 複製多行貼到 Excel。
    - ![09](https://hackmd.io/_uploads/BJrub7B_Jl.jpg)
    6. 匯出 CSV：
    - 點擊後可選擇存檔路徑。
    - 系統會以 UTF-8-SIG 編碼輸出，以兼容 Excel。




## 常見問題 (FAQ)
1. 為什麼執行時沒有反應，或程式凍結？

- 可能是網頁載入較久，或網路環境不穩。建議查看 time.sleep(3) 的等待時間是否需要調整，或改用 WebDriverWait 來等待特定元素載入。

2. 爬不到想要的資料該怎麼辦？

- 檢查該網頁是否使用大量動態載入 (JavaScript)，可能需要滾動頁面或特定互動才能顯示目標內容。
- 嘗試使用 開發者工具(F12) 檢視實際 DOM 位置與 className，調整 CSS Selector。

3. 刪除欄位失敗或刪除過久？

- 當資料量很大時，刪除欄位需要重新渲染表格。故使用多執行緒，避免 GUI 卡住。
- 也可考慮優化將 DataFrame 處理部分放在背景執行。

4. 為何匯出 CSV 後，中文亂碼？

- 預設使用 utf-8-sig 編碼，若是開啟檔案時遇到亂碼，請在 Excel 開啟時選擇 UTF-8 或相容的編碼。
- 或是可以在顯示所有資料時，使用Ctrl + C 複製貼在excel也可以解決亂碼問題

## 授權
