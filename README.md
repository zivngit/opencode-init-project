# opencode-init-project

OpenCode Agent Skill（`init-project`）：將 agents 協作文件模板（`docs/agents`、`.gitignore`、README）套用到新專案。

## 模板內容

- `docs/agents/AGENTS.md`、`TODO.md`、`CALL_GRAPH.md`、`reports/REPORT_TEMPLATE.md`
- `docs/temp/`（空目錄，暫存草稿用，已被 `.gitignore` 忽略）
- `.gitignore`（IDE、Python 建置產物、虛擬環境、環境變數、暫存）
- README（既有者只合併缺少的 SOP 與文件維護原則章節；不存在者以模板建立）

## 安裝

將 `init-project` 資料夾放到 OpenCode 的任一 skill 發現路徑：

| 層級 | 路徑 |
| --- | --- |
| 全域 | `~/.config/opencode/skills/init-project`（Unix）／ `%USERPROFILE%\.config\opencode\skills\init-project`（Windows） |
| 專案 | `.opencode/skills\init-project`（專案根目錄） |

快速安裝：

```bash
# Unix
git clone https://github.com/zivngit/opencode-init-project ~/.config/opencode/skills/init-project

# Windows (PowerShell)
git clone https://github.com/zivngit/opencode-init-project "$env:USERPROFILE\.config\opencode\skills\init-project"
```

也可 clone 到任意位置後，僅將 `init-project` 資料夾複製到上述路徑。

安裝完成後**重啟 OpenCode**，接著說「建立專案」、「初始化專案」或「套用模板」即可觸發。

## 行為保證

- 絕不覆蓋目標專案的既有內容：README／.gitignore 採合併追加、保留既有 git 歷史、不觸碰其他檔案。
- 套用完成會依模板在 `docs/agents/reports/` 產出工作報告並提交。
- skill 內容不熱重新載入，修改 `SKILL.md` 後需重啟 OpenCode。

## License

MIT（詳見 [LICENSE](LICENSE)）
