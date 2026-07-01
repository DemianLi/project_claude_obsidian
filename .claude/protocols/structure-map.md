# 結構總覽（⚡ = 薄索引，永遠先讀）

```
【知識庫 — KB_ROOT = CLAUDE.md 所在目錄（clone 到哪裡都自動成立，見 CLAUDE.md 開頭定義）】

projects/{專案}/
  00-overview.md
  01-requirements/  functional-index.md⚡  functional/{m}.md  scope.md（BEFORE CODING/`/cr` 依賴）  non-functional.md  _pending/_index.md⚡（QC頭）+ _pending/{ID}.md  _inferred/_index.md⚡（QC頭）+ _inferred/{ID}.md
  02-architecture/  arch-index.md⚡  system-design/{c}.md  api-contracts/index.md⚡  api-contracts/{g}.md  _legacy-analysis.md（擴充案，選配）
  03-client-context/  stakeholders.md（QC頭）  existing-system.md（QC頭）  domain-knowledge.md（QC頭）
  04-decisions/  ADR-index.md⚡  ADR-{ID}.md
  05-dev-notes/  _index.md⚡  {YYYY-MM-DD}-{主題}.md
  06-qa-testing/  bugs-active.md⚡  bugs/{BUG-ID}.md
  CHANGELOG.md
  collab/{initials}.md           （各工程師鎖定狀態，選配；有效類型見 knowledge/_schemas/collab.md）

knowledge/  patterns/index.md⚡  lessons-learned/index.md⚡  tech-stack/index.md⚡

wiki/  hot/{initials}.md⚡  index.md⚡  log.md  overview.md
  concepts/_index.md⚡   — 概念、框架、設計模式
  entities/_index.md⚡   — 技術、工具、第三方服務實體
  sources/_index.md⚡    — 閱讀/研究資料摘要
  questions/_index.md⚡  — 查詢後歸檔的好答案

.raw/  — 不可修改的原始文件（/ingest 的輸入來源）
_inbox/  _unassigned/

【程式碼 — CODE_ROOT = 程式碼實際所在目錄，父路徑不限】（獨立 repo，工程師自行 git 管理）
  實際 source code、設定檔、CLAUDE.md（薄版，由 /project-init 產生）

Obsidian 慣例：詳見 {KB_ROOT}/.claude/protocols/wiki-layer.md
```

**指令子文件路徑慣例**：`.claude/commands/*.md`（dispatcher）內所有 `_xxx/file.md` 形式的路徑，皆相對於 `{KB_ROOT}/.claude/impl/`，例如 `_query/standard.md` 實際是 `{KB_ROOT}/.claude/impl/_query/standard.md`。這是全部 17 個指令一致採用的簡寫，不是個別檔案的疏漏。
