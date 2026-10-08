# Vault 结构

初始化、检查、修复或解释 CODEBRAIN vault 时，使用本 reference。

## 根目录

首次使用要求用户先新建 Obsidian Vault 并提供完整路径。路径选择依次为当前明确路径、当前项目已确认且可访问的路径、`CODEBRAIN_HOME`、已存在的 `~/CODEBRAIN`。路径无效或无明确选择而存在冲突时先询问，不静默换目录。初始化只补充缺失模板，保留已有文件和 `.obsidian/`。

除文件名、路径、命令、代码标识符和外部错误原文外，vault 中面向人阅读的标题、字段名和正文必须使用简体中文。

预期结构：

```text
CODEBRAIN/
  VAULT_INDEX.md
  _templates/
  00_Inbox/
    raw/
    triaged/
  01_Projects/
    _TEMPLATE/
    <project-slug>/
  02_Agents/
  03_Knowledge/
    patterns/
    references/
  04_Global/
  99_Archive/
```

## 根目录文件

- `VAULT_INDEX.md`：唯一总入口。列出活跃项目、当前交接文档链接、P0 工作和最近更新。
- `_templates/`：可复用 Markdown 模板。不要把模板文件当作活跃项目状态。
- `00_Inbox/`：来自用户、其他 AI、飞书、文章、转录或聊天导出的原始/已分拣材料。
- `02_Agents/`：agent 能力边界和投递协议。不要把长运行日志放这里。
- `03_Knowledge/`：只放跨项目可复用模式和参考资料。
- `04_Global/`：跨项目任务、日志、handoff 索引和对话索引。
- `99_Archive/`：已结束项目和过期材料，不进入日常读取路径。

## 项目核心

每个活跃项目位于 `01_Projects/<project-slug>/`，包含六个核心文件：

- `PROJECT_INDEX.md`：目标、代码根目录、read-first 文件、模块地图、当前状态和链接。
- `TASKS.md`：按 P0 到 Pn 排序的任务，包含状态、验收标准、证据和链接。
- `DECISIONS.md`：已确认决策、原因、被拒绝方案、影响和重新评估触发条件。
- `PHASE_LOG.md`：只追加的阶段摘要，记录证据和下一步。
- `HANDOFF.md`：给下一次 Codex 或人类接手的短交接文档。
- `LESSONS.md`：已验证、可复用的经验，不放原始观察。

项目辅助目录：

- `_inbox/`：等待分拣的项目级原始材料。
- `conversations/`：对话摘要和链接。
- `logs/`：只有需要证据时才放较长日志。

## 读取顺序

读取代码前，按顺序读取：

1. `VAULT_INDEX.md`
2. `01_Projects/<project-slug>/PROJECT_INDEX.md`
3. `HANDOFF.md`
4. `TASKS.md`
5. 最近相关的 `PHASE_LOG.md` 条目
6. 这些文档显式链接的文件

除非索引缺失或过期，否则避免全 vault 扫描。

## 双链规则

- 任务应链接决策、phase log 和证据。
- 决策应链接触发它的 phase 或 proposal。
- 阶段日志应链接涉及文件和验证证据。
- 交接文档应链接当前 P0/P1 任务和最新阶段日志。
- 需要时使用稳定项目标签：`#project/<slug>`、`#type/handoff`、`#status/active`。

v1 不依赖 Dataview 或任何 Obsidian 插件。
