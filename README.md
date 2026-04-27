
---

## 6. Chrome 擴充套件安裝 / Chrome Extension Installation

### 繁體中文

#### 下載擴充套件

1. 點擊應用右上角「**下載 Chrome 擴充**」按鈕
2. 瀏覽器會下載一個 `.txt` 檔案，內含所有擴充套件程式碼

#### 建立擴充套件資料夾

在您的電腦上建立一個資料夾（例如 `mcp-extension`），並在其中建立以下檔案：

```
mcp-extension/
├── manifest.json      ← 擴充套件設定檔
├── background.js      ← 背景服務工作者（MCP 核心）
├── content.js         ← 注入網頁的腳本
└── popup.html         ← 擴充套件彈出視窗
```

將下載的 `.txt` 檔案中對應區段的程式碼，分別複製到各檔案中。

#### 安裝到 Chrome

1. 開啟 Chrome，在網址列輸入：`chrome://extensions/`
2. 開啟右上角的「**開發人員模式**」開關
3. 點選「**載入未封裝項目**」
4. 選擇您建立的 `mcp-extension` 資料夾
5. 擴充套件圖示出現在工具列即代表安裝成功

#### 驗證安裝

點擊工具列的擴充套件圖示，彈出視窗顯示「MCP 協定已啟用」即表示正常運作。  
點擊「測試 MCP 擷取」按鈕可驗證功能是否正常。

### English

#### Download the Extension

1. Click the "**下載 Chrome 擴充 / Download Chrome Extension**" button in the top-right
2. A `.txt` file containing all extension code will be downloaded

#### Create the Extension Folder

Create a folder on your computer (e.g., `mcp-extension`) with the following files:

```
mcp-extension/
├── manifest.json      ← Extension configuration
├── background.js      ← Service worker (MCP core)
├── content.js         ← Page injection script
└── popup.html         ← Extension popup UI
```

Copy the corresponding code sections from the downloaded `.txt` file into each file.

#### Install in Chrome

1. Open Chrome, navigate to: `chrome://extensions/`
2. Enable **Developer mode** toggle (top-right)
3. Click **"Load unpacked"**
4. Select your `mcp-extension` folder
5. The extension icon appearing in the toolbar confirms successful installation

#### Verify Installation

Click the extension icon in the toolbar. If the popup shows "MCP 協定已啟用 / MCP Protocol Active", it's working correctly.  
Click "測試 MCP 擷取 / Test MCP Fetch" to verify functionality.

---

## 7. MCP 運作原理 / How MCP Works

### 繁體中文

**MCP（Model Context Protocol）** 是一種讓 AI 模型能夠安全存取外部工具與資料來源的標準協定。

在本應用中，MCP 的運作流程如下：

```
① 用戶提問
② Agent 建構 Google Search URL（udm=14）
③ Chrome Extension 接收 MCP 請求
④ Extension 的 background.js 使用 scripting API 擷取頁面
⑤ content.js 提取頁面文字內容（最多 5,000 字元）
⑥ 擷取結果回傳給 Agent
⑦ Agent 傳送給 LLM 進行分析
⑧ LLM 生成回答輸出給用戶
```

**udm=14 的作用：**  
`udm=14` 是 Google Search 的一個參數，代表「網頁搜尋精準模式」，可以過濾掉 AI 生成內容、廣告等雜訊，取得更純粹的網頁搜尋結果。

### English

**MCP (Model Context Protocol)** is a standard protocol that allows AI models to securely access external tools and data sources.

In this application, MCP works as follows:

```
① User asks a question
② Agent builds Google Search URL (udm=14)
③ Chrome Extension receives MCP request
④ background.js uses scripting API to fetch the page
⑤ content.js extracts page text content (up to 5,000 chars)
⑥ Fetched content is returned to the Agent
⑦ Agent sends it to LLM for analysis
⑧ LLM generates an answer for the user
```

**What udm=14 does:**  
`udm=14` is a Google Search parameter representing "Web Search Precision Mode". It filters out AI-generated content, ads, and noise — returning cleaner, more authentic web search results.

---

## 8. System Prompt 架構 / System Prompt Architecture

### 繁體中文

本應用參考影片「以 OpenClaw 為例介紹 AI Agent 的運作原理」的架構設計，System Prompt 由以下模組組成：

| 檔案 | 用途 |
|------|------|
| `SOUL.md` | 定義 Agent 的核心價值觀與人格特質 |
| `IDENTITY.md` | 定義 Agent 的角色、能力與限制 |
| `USER.md` | 儲存使用者的偏好、背景與目標 |
| `MEMORY.md` | 記憶儲存策略（短期、長期、向量記憶） |
| `AGENTS.md` | 規範 Agent 的決策流程與工具呼叫邏輯 |

可在左側導覽列點擊各模組名稱查看詳細內容。

### English

This application's design is inspired by the "OpenClaw AI Agent Architecture" video. The System Prompt is composed of the following modules:

| File | Purpose |
|------|---------|
| `SOUL.md` | Defines the Agent's core values and personality |
| `IDENTITY.md` | Defines the Agent's role, capabilities, and limitations |
| `USER.md` | Stores user preferences, background, and goals |
| `MEMORY.md` | Memory storage strategy (short-term, long-term, vector) |
| `AGENTS.md` | Governs the Agent's decision-making and tool-calling logic |

Click each module name in the left sidebar to view its details.

---

## 9. 常見問題 / FAQ

### 繁體中文

**Q：為什麼 Agent 沒有真的搜尋到結果？**  
A：完整的 MCP 網頁擷取功能需要安裝 Chrome 擴充套件。未安裝時，Agent 會根據自身知識庫回答，並顯示對應的 Google Search URL 供您手動查看。

**Q：可以在手機上使用嗎？**  
A：可以。本應用為響應式設計，支援手機瀏覽器。但 Chrome 擴充套件功能僅限桌機版 Chrome。

**Q：我的搜尋記錄會上傳到伺服器嗎？**  
A：不會。搜尋記錄僅儲存在您本機瀏覽器的 `localStorage`，不會傳送到任何伺服器。

**Q：udm=14 是什麼意思？**  
A：這是 Google Search 的精準網頁搜尋參數，可以過濾掉 AI 生成內容與廣告，取得更純粹的搜尋結果。

**Q：如何清除對話或搜尋記錄？**  
A：對話視窗右上角有「清除對話」按鈕；搜尋記錄頁面右上角有「清除記錄」按鈕。

### English

**Q: Why doesn't the Agent actually retrieve search results?**  
A: Full MCP web fetching requires the Chrome Extension to be installed. Without it, the Agent answers from its knowledge base and shows the Google Search URL for you to check manually.

**Q: Can I use this on mobile?**  
A: Yes. The app is responsive and works on mobile browsers. However, the Chrome Extension feature is only available on desktop Chrome.

**Q: Will my search history be uploaded to a server?**  
A: No. Search history is stored only in your browser's `localStorage` and is never sent to any server.

**Q: What does udm=14 mean?**  
A: It's a Google Search precision parameter that filters out AI-generated content and ads, returning cleaner web search results.

**Q: How do I clear the chat or search history?**  
A: Use the "清除對話 / Clear Chat" button in the top-right of the chat view; use "清除記錄 / Clear History" in the search history view.

---

## 10. 技術規格 / Technical Specifications

### 繁體中文

| 項目 | 規格 |
|------|------|
| **檔案格式** | 單一 HTML 檔案（無需安裝） |
| **相依套件** | Marked.js（CDN）、Google Fonts |
| **LLM API** | Anthropic Claude Sonnet（需網路連線） |
| **搜尋引擎** | Google Search（udm=14 精準模式） |
| **MCP 實作** | Chrome Extension（Manifest V3） |
| **資料儲存** | localStorage（本機，無伺服器） |
| **瀏覽器支援** | Chrome 88+、Edge 88+、Firefox 89+ |
| **響應式支援** | 手機（≥320px）、平板、桌機 |

### English

| Item | Specification |
|------|--------------|
| **File Format** | Single HTML file (no installation needed) |
| **Dependencies** | Marked.js (CDN), Google Fonts |
| **LLM API** | Anthropic Claude Sonnet (requires internet) |
| **Search Engine** | Google Search (udm=14 precision mode) |
| **MCP Implementation** | Chrome Extension (Manifest V3) |
| **Data Storage** | localStorage (local, no server) |
| **Browser Support** | Chrome 88+, Edge 88+, Firefox 89+ |
| **Responsive** | Mobile (≥320px), Tablet, Desktop |

---

## 授權與參考 / License & References

- 參考專案 Reference：[kaojarher.github.io/MCPRPA/](https://kaojarher.github.io/MCPRPA/)
- MCP 協定規範：[Model Context Protocol Spec](https://modelcontextprotocol.io/)
- Google Search 精準模式：`https://www.google.com/search?q={query}&udm=14`

---

*本說明文件以繁體中文為主要語言，並附有英文對照。*  
*This document is primarily written in Traditional Chinese with English translations.*
