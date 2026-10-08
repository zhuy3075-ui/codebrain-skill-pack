# 安装与首次使用

## 1. 先新建 Obsidian Vault

首次使用本包，先在 Obsidian 中创建专门用于 CODEBRAIN 的 Vault，记下**完整绝对路径**。例如 Windows 的 `D:\Obsidian\CODEBRAIN`，或 macOS / Linux 的 `/完整路径/CODEBRAIN`。路径中的空格和中文可原样告诉技能。

Vault 是个人项目记忆库，不是技能安装目录，也不是此 GitHub 仓库。Obsidian 创建的 `.obsidian/` 配置应保留。

## 2. 复制技能目录

将仓库的 `skills/codebrain-memory/` 整个文件夹复制到 `~/.codex/skills/codebrain-memory/`；其他技能按需安装到 `~/.codex/skills/`。`~` 表示当前用户目录，Windows 通常对应 `%USERPROFILE%`。

完整复制 `SKILL.md` 及技能内部的 `references/`、`assets/`、`agents/`。目标已存在时先比较并备份，再决定更新。新开会话或重启客户端后，检查技能是否在当前会话中可见。

## 3. 将 Vault 路径告诉技能

首次使用必须向 `codebrain-memory` 提供刚创建的 Vault 的完整路径；要初始化时同时明确要求初始化。例如：

```text
使用 $codebrain-memory。
我已在 Obsidian 中新建 Vault，完整路径为：D:\Obsidian\CODEBRAIN
请在该目录初始化 CODEBRAIN 模板，保留已有文件和 .obsidian 配置。
完成后检查目录，并报告实际使用的 Vault 路径。
```

技能先检查这个明确路径是否存在、是否为目录。如果只告知路径，会先做只读检查；明确要求初始化后，才把 `assets/vault-template/` 中缺失的文件复制进去。已有同名文件不覆盖。

提供的路径不存在或无法访问时，应说明问题并等待修正，不能悄悄换到默认目录。未提供首次路径时，技能应提醒先新建 Vault 并索取路径。

## 4. 确认初始化结果

Vault 根目录应直接包含以下结构，而不是多嵌套一层 `vault-template/`：

```text
CODEBRAIN/
├── VAULT_INDEX.md
├── 00_Inbox/
├── 01_Projects/_TEMPLATE/
├── 02_Agents/
├── 03_Knowledge/
├── 04_Global/
├── 99_Archive/
└── _templates/
```

检查 `01_Projects/_TEMPLATE/` 中的六个核心文档：`PROJECT_INDEX.md`、`TASKS.md`、`DECISIONS.md`、`PHASE_LOG.md`、`HANDOFF.md`、`LESSONS.md`。需要项目记忆时，再让技能为真实项目创建目录，并更新总索引。

## 5. 后续会话复用路径

聊天里提供的路径不会自动成为永久配置。以后可在新会话中再次提供路径，或者自行把 `CODEBRAIN_HOME` 设置为该路径，确保启动 Codex 的进程能读取到它。技能不会因为用户告知路径就自行修改系统环境变量、全局协议或创建符号链接。

后续路径选择顺序：

1. 当前用户明确提供的路径。
2. 当前项目已确认且仍可访问的 Vault 路径。
3. `CODEBRAIN_HOME`。
4. 已存在的 `~/CODEBRAIN`。

多个候选路径冲突且无法确定时，先询问；明确路径失效时先修正。首次初始化不能用项目内备用目录替代新建 Vault。项目内 `docs/codex/<task-slug>/` 只可在用户明确选择不用 Vault 时使用。

## 6. 按需合并 AGENTS 协议

这一步可选，显式调用 `codebrain-memory` 不要求先安装两份协议。当前两份模板正文完全相同，区别是放置范围，不是功能不同或两个独立 Agent。

- [全局模板](../templates/agents/AGENTS.global.md)：供合并到 `~/.codex/AGENTS.md` 时参考。
- [项目模板](../templates/agents/AGENTS.project.md)：供合并到具体项目的 `AGENTS.md` 时参考。

阅读后按需合并，不直接覆盖已有规则。模板中提及的技能、插件、连接器和权限，需要实际可用后才能使用。

建议先在一个项目中合并项目模板；需要多个项目共用时，再提取通用规则到全局文件，项目文件只写差异。合并后的目标文件名为 `AGENTS.md`，不能仅保留模板的 `.global.md` 或 `.project.md` 名称就视作已安装。若自定义了 `CODEX_HOME`，全局文件应位于该配置目录。范围说明及官方参考见 [README](../README.md#两份-agents-文档有什么区别)。

## 常见问题

**记忆库会在 Codex 关闭时继续更新吗？** 不会。本包不提供后台服务或调度器。

**所有技能都必须安装吗？** 不需要。可从 `codebrain-memory` 开始，再按任务选择[其他技能](skills.md)。

**预算文件在哪里？** `loop-budget` 等技能定义了输入约定，实际预算和运行日志需要按项目准备。本包没有完整 Loop 启动器。

**看不到技能怎么办？** 先检查技能目录及 `SKILL.md`，再确认已新开会话；加载设置以实际客户端为准。
