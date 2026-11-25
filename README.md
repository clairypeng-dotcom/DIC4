# DIC4 — Food Guardian ICEIB IEEE Conference Paper Workspace

本儲存庫用於撰寫與維護 **Food Guardian** 計畫的 **ICEIB（IEEE International Conference on Electronic Communications, Internet of Things and Big Data）** IEEE 會議論文（依據 [iceib.asia](https://www.iceib.asia/) 規範：`IEEEtran` 雙欄會議格式、英文撰寫、4–8 頁），並整合原始專案設計文件與 OpenSpec 驗收規格。

---

## 目錄結構｜Repository Structure

```text
DIC4/
├── README.md                                       # 本說明文件
├── .gitmodules                                     # Submodule 設定
├── ICEIB paper/                                    # 模組化 IEEEtran 論文專案（建議以此為主）
│   ├── main.tex                                    # LaTeX 主進入點（Overleaf / pdflatex 使用）
│   ├── main.txt                                    # 與 main.tex 同步之純文字入口
│   ├── 000-Abstract.tex                            # Abstract 與 Index Terms
│   ├── 001-Introduction.tex                        # I. Introduction
│   ├── 002-Related Work.tex                        # II. Related Work（含文獻比較表）
│   ├── 003-Proposed Design.tex                     # III. Proposed Design（架構圖、資料表、演算法與公式）
│   ├── 004-Experiment.tex                          # IV. Experiment（實作、OpenSpec 驗收、初步結果與對照實驗規劃）
│   ├── 005-Conclusion.tex                          # V. Conclusion
│   └── 006-Reference.tex                           # IEEE 格式參考文獻 [1]–[11]
├── DIC3-Project-Proposal-Refactor-using-Openspec/  # Submodule：原修訂報告、系統設計與 OpenSpec 規格
├── myRef/                                          # 寫作風格與參考資料存放目錄
└── IGIB paper/                                     # 早期單檔草稿保留目錄
```

---

## 快速使用｜Quick Start

### 1. 下載儲存庫（含 Submodule）

```bash
git clone --recurse-submodules https://github.com/clairypeng-dotcom/DIC4.git
cd DIC4
```

若已 clone 但未拉取 submodule，請執行：

```bash
git submodule update --init --recursive
```

### 2. 在 Overleaf / 本機 LaTeX 編譯論文

- 將 `ICEIB paper/` 內所有 `.tex` 檔案匯入 Overleaf（或透過 `overleaf-latex-mcp` + `ols` 同步）。
- 將主文件（Main document）設為 `main.tex`，編譯器選擇 **`pdfLaTeX`**。
- 內建圖表使用 `TikZ` 與 `algorithmic` 繪製，無需額外外部圖片檔即可直接編譯。

> **投稿前提醒**：請在 `ICEIB paper/main.tex`（與 `main.txt`）的 `\author{...}` 區塊補齊正式英文姓名拼寫、系所／學校機構名稱與聯絡信箱。

### 3. OpenSpec 規格檢查（位於 Submodule）

```bash
cd DIC3-Project-Proposal-Refactor-using-Openspec
openspec status --change validate-food-guardian-workflow
openspec validate validate-food-guardian-workflow --strict
```

---

## 論文驗證數據摘要（對齊 `DESIGN.md` 與 OpenSpec）

- **單元測試**：`pytest tests -q` 全數 **40 / 40** 通過。
- **固定評估套件（30 組案例）**：離線決定性規則與靜態檢查 **25 PASS**、**5 NOT_RUN**（需即時 LLM 多工具呼叫）。
- **Gemini Live 多工具初測（排除 RAG 相依題 `MUL-02`、`MUL-04`）**：嘗試 **3 / 3**、API 成功率 **3 / 3 (100%)**、有效工具選擇準確率 **3 / 3 (100%)**、平均延遲 **11.71 秒**（含 1 次有限退避重試）。
- **待完成驗證**：Live RAG 引用支持度（`MUL-02`、`MUL-04`）、與一般 LLM 之配對基準比較實驗、跨模組整合人工驗收及長期家庭減浪成效觀察。
