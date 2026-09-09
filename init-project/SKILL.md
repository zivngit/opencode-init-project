---
name: init-project
description: 將 agents 協作模板（docs/agents、.gitignore、README）套用到新專案。Use when the user says 「建立專案」、「初始化專案」、「套用模板」、「加入 agents 模板」or asks to init/bootstrap a new project with this template.
license: MIT
compatibility: opencode
metadata:
  version: 1.0.0
---

# 套用 Agents 專案模板

將本機模板專案的 agents 協作文件套用到目標專案。

- **模板來源**：本 SKILL.md 所在資料夾（載入 skill 時提供的 Base directory）
- **套用內容**：`docs/agents/AGENTS.md`、`docs/agents/TODO.md`、`docs/agents/CALL_GRAPH.md`、`docs/agents/reports/REPORT_TEMPLATE.md`、`docs/temp/`（空資料夾）、`.gitignore`、README（視目標現況）

## 流程

1. **確認目標專案**
   - 預設目標為目前工作目錄；若目錄不存在則先建立。
   - 專案名稱預設取目錄名稱；與使用者意圖不符時先向使用者確認。
2. **檢查模板來源**
    - 確認 `<Base directory>\docs\agents` 存在（Base directory 即本 SKILL.md 所在資料夾）；找不到時詢問使用者模板的實際位置。
3. **檢查目標現況並決定策略**（絕不覆蓋既有內容）

   | 目標現況 | 處理方式 |
   | --- | --- |
   | `docs/agents` 已存在 | 停止，詢問使用者要合併、跳過或改名 |
   | `README.md` 已存在 | 保留原文；若缺少「Agent 工作週期 (SOP)」與「文件維護原則」章節則附至結尾，避免重覆 |
   | `README.md` 不存在 | 以模板 README 建立：填入專案名稱，移除「使用方法」中複製模板的步驟 |
   | `.gitignore` 已存在 | 僅逐行追加模板中缺少的規則，不重覆、不改寫原有規則 |
   | `.gitignore` 不存在 | 直接複製模板的 `.gitignore` |
   | git 倉庫已存在 | 不執行 `git init`，保留既有歷史 |
   | git 倉庫不存在 | 執行 `git init` |
   | `docs/` 已有其他內容 | 只建立 `docs/agents` 與 `docs/temp`（空資料夾），不觸碰其他檔案 |

4. **複製模板檔案**
   - 複製 `docs/agents` 的 4 個核心文件；`reports/` 只複製 `REPORT_TEMPLATE.md`。
   - 建立 `docs/temp/` 空資料夾（複製工具可能略過空目錄，需確認存在）。
   - 不得複製模板的 `.git`（模板目錄本身可能受版本控制）。
5. **替換佔位符**：將新複製文件中的所有 `<專案名稱>` 替換為實際專案名稱。
6. **提交**：`git add` 新增與修改的檔案，建立具描述性的 commit（新專案 AGENTS.md 要求每次改動都要 commit）。
7. **工作報告**：依新專案 `docs/agents/reports/REPORT_TEMPLATE.md` 格式產出 `YYYY-MM-DD-NNN-init-project.md` 報告（NNN 依該目錄既有報告總數 + 1 累計連編，新專案為 `001`；報告本身不列入文件異動表），再建立 commit。
8. **回報**：列出新增/合併的檔案、commit hash、需使用者後續處理的事项（如 README 合併處）。

## 注意

- 全程不得刪除或覆蓋目標專案的既有檔案與 git 歷史。
- 本資料夾的 `SKILL.md` 不屬於模板內容，不得複製到目標專案。
- 不得將產出的報告或 git 歷史寫入模板目錄（模板維持純檔案集合）。
- `docs/temp/` 隨模板一併建立；其內容已被 `.gitignore` 忽略，不納入版本控制。
- 若目標專案根目錄另有自己的 `AGENTS.md`，先告知使用者可能存在規範衝突，經確認後再繼續。
