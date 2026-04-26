# AI Agent Studio — 使用說明 / User Guide

> 版本 Version：v0.3 · MCP  
> 語言 Language：繁體中文 / English  
> 最後更新 Last Updated：2026-04-26

---

## 目錄 / Table of Contents

1. [專案簡介 / Project Overview](#1-專案簡介--project-overview)
2. [系統架構 / System Architecture](#2-系統架構--system-architecture)
3. [如何開始使用 / Getting Started](#3-如何開始使用--getting-started)
4. [介面說明 / Interface Guide](#4-介面說明--interface-guide)
5. [如何輸入問題 / How to Input](#5-如何輸入問題--how-to-input)
6. [Chrome 擴充套件安裝 / Chrome Extension Installation](#6-chrome-擴充套件安裝--chrome-extension-installation)
7. [MCP 運作原理 / How MCP Works](#7-mcp-運作原理--how-mcp-works)
8. [System Prompt 架構 / System Prompt Architecture](#8-system-prompt-架構--system-prompt-architecture)
9. [常見問題 / FAQ](#9-常見問題--faq)
10. [技術規格 / Technical Specifications](#10-技術規格--technical-specifications)

---

## 1. 專案簡介 / Project Overview

### 繁體中文

**AI Agent Studio** 是一個以單一 HTML 檔案實作的響應式 AI Agent 應用程式。  
整合了 **Google Search**（udm=14 精準模式）與 **MCP（Model Context Protocol）** 協定，讓 AI 能夠自動搜尋網路並擷取頁面內容進行分析。

**主要特色：**
- 無需安裝後端伺服器，單一 `.html` 檔案即可運行
- 透過 Google Search `udm=14` 精準搜尋模式送出查詢
- 以 Chrome 擴充套件實作 MCP 協定，擷取網頁內容
- 完整的 System Prompt 架構視覺化（SOUL / IDENTITY / USER / MEMORY / AGENTS）
- 搜尋記錄自動儲存（localStorage）
- 支援手機與桌機的響應式佈局

### English

**AI Agent Studio** is a responsive AI Agent application implemented as a single HTML file.  
It integrates **Google Search** (udm=14 precision mode) with the **MCP (Model Context Protocol)** to enable AI to automatically search the web and fetch page content for analysis.

**Key Features:**
- No backend server required — runs as a single `.html` file
- Sends queries via Google Search `udm=14` precision mode
- Implements MCP protocol via Chrome Extension to fetch web content
- Full System Prompt architecture visualization (SOUL / IDENTITY / USER / MEMORY / AGENTS)
- Auto-saves search history (localStorage)
- Responsive layout for mobile and desktop

---

## 2. 系統架構 / System Architecture

### 繁體中文

```
用戶輸入問題
     │
     ▼
建構 Google Search URL
https://www.google.com/search?q={查詢內容}&udm=14
     │
     ▼
Chrome Extension (MCP 協定)
擷取搜尋結果頁面內容
     │
     ▼
LLM 分析（Anthropic API）
整合網頁內容 + 回答問題
     │
     ▼
輸出結果給用戶
```

### English

```
User Input
     │
     ▼
Build Google Search URL
https://www.google.com/search?q={query}&udm=14
     │
     ▼
Chrome Extension (MCP Protocol)
Fetch search result page content
     │
     ▼
LLM Analysis (Anthropic API)
Integrate web content + answer question
     │
     ▼
Output result to user
```

---

## 3. 如何開始使用 / Getting Started

### 繁體中文

**步驟一：下載檔案**
1. 下載 `ai-agent-mcp.html` 檔案到您的電腦

**步驟二：用 Chrome 開啟**
1. 開啟 Google Chrome 瀏覽器
2. 將 `ai-agent-mcp.html` 拖曳到 Chrome 視窗中，或雙擊檔案開啟

**步驟三：安裝 Chrome 擴充套件（建議）**
1. 點選右上角「下載 Chrome 擴充」按鈕
2. 依照第 6 節的安裝說明完成安裝
3. 安裝後即可使用完整 MCP 功能

**步驟四：開始對話**
1. 在底部輸入框輸入您的問題
2. 按 `Enter` 或點擊送出按鈕
3. Agent 會自動搜尋並回覆

### English

**Step 1: Download the file**
1. Download `ai-agent-mcp.html` to your computer

**Step 2: Open with Chrome**
1. Open Google Chrome browser
2. Drag `ai-agent-mcp.html` into Chrome, or double-click to open

**Step 3: Install Chrome Extension (Recommended)**
1. Click the "下載 Chrome 擴充 / Download Chrome Extension" button in the top-right
2. Follow the installation instructions in Section 6
3. Once installed, full MCP functionality is enabled

**Step 4: Start Chatting**
1. Type your question in the input box at the bottom
2. Press `Enter` or click the send button
3. The Agent will automatically search and reply

---

## 4. 介面說明 / Interface Guide

### 繁體中文

| 區域 | 說明 |
|------|------|
| **頂部工具列** | 顯示應用名稱、連線狀態、下載擴充套件按鈕 |
| **左側導覽** | 切換各功能模組（對話、System Prompt、搜尋記錄、擴充套件、身分模組） |
| **Pipeline 狀態列** | 即時顯示 Agent 執行進度：輸入 → 搜尋 → MCP 擷取 → LLM → 輸出 |
| **對話視窗** | 顯示用戶與 Agent 的對話內容 |
| **工具列（輸入上方）** | 切換 Google Search / MCP 擷取 / 深度分析等工具 |
| **輸入框** | 輸入問題的地方 |

### English

| Area | Description |
|------|-------------|
| **Top Toolbar** | Shows app name, connection status, extension download button |
| **Left Sidebar** | Switch between modules (Chat, System Prompt, History, Extension, Identity) |
| **Pipeline Status Bar** | Real-time display of Agent progress: Input → Search → MCP → LLM → Output |
| **Chat Window** | Shows conversation between user and Agent |
| **Tool Chips (above input)** | Toggle Google Search / MCP Fetch / Deep Analysis tools |
| **Input Box** | Where you type your questions |

---

## 5. 如何輸入問題 / How to Input

### 繁體中文

#### 基本輸入方式

1. **點擊底部輸入框**（提示文字：「輸入問題，Agent 將自動 Google 搜尋並分析...」）
2. 輸入您的問題，例如：
   - `AI Agent 是什麼？`
   - `2024 年台灣 AI 發展趨勢`
   - `Python 如何讀取 CSV 檔案`
3. 送出問題：
   - 按下鍵盤 **`Enter`** 鍵（換行請用 `Shift + Enter`）
   - 或點擊輸入框右側的 **藍色箭頭送出按鈕**

#### 工具選項

輸入框上方有三個工具開關，點擊可切換啟用/關閉：

| 工具 | 說明 | 預設 |
|------|------|------|
| **Google Search** | 透過 `udm=14` 精準模式搜尋 | ✅ 啟用 |
| **MCP 擷取** | 使用 Chrome Extension 擷取頁面內容 | ❌ 關閉 |
| **深度分析** | 進行更詳細的多步驟分析 | ❌ 關閉 |

#### 查看搜尋 URL

每次送出問題後，對話視窗會顯示：
- 🔍 實際送出的 Google Search URL（可點擊開啟）
- 🌐 MCP 擷取狀態與結果連結

#### 重用歷史搜尋

1. 點擊左側「搜尋記錄」
2. 點擊任一歷史記錄，即可重新搜尋相同問題

### English

#### Basic Input Method

1. **Click the input box** at the bottom (placeholder: "輸入問題，Agent 將自動 Google 搜尋並分析...")
2. Type your question, for example:
   - `What is an AI Agent?`
   - `AI development trends in 2024`
   - `How to read CSV files in Python`
3. Submit your question:
   - Press **`Enter`** key (use `Shift + Enter` for new line)
   - Or click the **blue arrow send button** on the right

#### Tool Options

Three tool toggles are available above the input box:

| Tool | Description | Default |
|------|-------------|---------|
| **Google Search** | Search via `udm=14` precision mode | ✅ On |
| **MCP Fetch** | Fetch page content via Chrome Extension | ❌ Off |
| **Deep Analysis** | Perform detailed multi-step analysis | ❌ Off |

#### Viewing the Search URL

After each submission, the chat shows:
- 🔍 The actual Google Search URL sent (clickable)
- 🌐 MCP fetch status and result link

#### Reusing Search History

1. Click "搜尋記錄 / Search History" in the sidebar
2. Click any history item to re-run that search

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
