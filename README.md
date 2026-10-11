# ∑ 數學公式語法轉換器（Math Syntax Converter）

貼上整段筆記，自動偵測公式語法，一鍵轉換成 **LaTeX／Markdown／GitHub Markdown／MathML／Typst**。

🔗 **線上使用：** https://duck1101.github.io/math-converter/

## 為什麼做這個工具

我用 ChatGPT 輔助學習，並用 Obsidian 做筆記。但 ChatGPT 的公式是用 `\( … \)`、`\[ … \]` 包住，Obsidian 卻只認得 `$ … $`、`$$ … $$`。
而且在 Markdown 裡，`\` 是跳脫字元，`\(` 會被當成普通的括號，所以每次複製都要手動修改。
這個工具可以把整段筆記裡的公式一次轉好，也支援 MathML、Typst 這些寫法完全不同的公式語言。

## 功能

- **整段筆記轉換**：文字和公式混在一起也沒問題，只會轉換公式的部分。
- **自動偵測來源語法**：判斷錯了也可以手動指定。
- **5 種語法雙向轉換**：

  | 語法 | 行內公式 | 獨立公式 |
  |---|---|---|
  | LaTeX | `\( … \)` | `\[ … \]`、`\begin{equation}` 等環境 |
  | Markdown | `$…$` | `$$…$$` |
  | GitHub Markdown | `` $`…`$ `` | ` ```math ` 區塊 |
  | MathML | `<math>…</math>` | `<math display="block">` |
  | Typst | `$x$` | `$ x $` |

- **合併連續的獨立公式**：把好幾個連續的 `\[ … \]` 合併成一組 `gather`（置中）或 `align`（等號對齊）。
- **即時預覽**：用 KaTeX 顯示公式的實際樣子，方便確認有沒有轉壞。
- **統計資訊**：顯示行內公式、獨立公式的數量，以及合併的組數、成功和失敗的數量。
- **一鍵複製**轉換結果。
- **特殊處理**：
  - 金額（例如 `$100`）不會被轉換。
  - 程式碼區塊裡的內容不會被轉換。
  - 自動修正 `$ x $` 內側多餘的空白。
  - 轉換失敗的公式會保留原文並標示出來。

## 使用方式

1. 打開[線上網頁](https://duck1101.github.io/math-converter/)，或直接用瀏覽器開啟 `index.html`。
2. 在左邊貼上筆記，也可以點「範例」按鈕載入範例筆記。
3. 在上方選擇要轉成的目標語法。
4. 右邊會即時顯示轉換結果，按「📋 複製」即可複製。

## 轉換原理

以 LaTeX 當作中間格式：

```
來源語法 → LaTeX → 目標語法
```

| 轉換 | 使用的工具 |
|---|---|
| LaTeX → MathML、預覽 | [KaTeX](https://katex.org/) |
| MathML → LaTeX | [mathml-to-latex](https://github.com/asnunes/mathml-to-latex) |
| LaTeX ↔ Typst | [tex2typst](https://github.com/qwinsi/tex2typst) |
| 外框互換 | 自己寫的正規表示式 |

## 技術

- 單一 `index.html`，HTML、CSS、JavaScript 都寫在同一個檔案裡。
- 外部套件從 jsDelivr CDN 載入，使用時需要連網。
- 部署在 GitHub Pages。

## 檔案說明

| 檔案 | 說明 |
|---|---|
| `index.html` | 網頁主程式 |
| `規格書.md` | 功能規格與開發過程紀錄 |
| `README.md` | 本說明文件 |

## 已知限制

- 轉成 LaTeX、Markdown、GitHub 時只換外框，不檢查公式本身有沒有寫錯。寫錯的公式會在預覽區顯示紅字。
- 轉成 Typst 或 MathML 時，比較少見的符號可能轉得不完全。
- `gather`、`align` 在某些軟體裡會自動加上公式編號。

---

本專案透過 Vibe Coding（與 AI 討論規格、反覆修改）完成。
