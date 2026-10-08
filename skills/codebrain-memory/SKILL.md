---
name: codebrain-memory
description: "全局 CODEBRAIN / Obsidian 项目记忆工作流。任务涉及编码、项目工作、仓库上下文、计划、规格说明、任务清单、阶段日志、交接文档、决策、经验、Loop Engineering、上下文管理、技术方案评估、初始化或更新 PROJECT_INDEX/TASKS/DECISIONS/PHASE_LOG/HANDOFF/LESSONS、读取 ~/CODEBRAIN、创建项目记忆、准备最终交接或分享 Codex loop 记忆方法时自动使用。"
---

# CODEBRAIN 项目记忆

使用这个 skill，让 Codex 的工程工作依赖一套小而稳定的长期记忆系统，而不是每次全仓扫描或依赖聊天历史。

首次使用前，用户需要先在 Obsidian 中新建一个专用 Vault 文件夹，并把完整绝对路径告诉本 skill。缺少路径时，先索取路径，不直接写入默认目录。

## 首次初始化与路径选择

- 优先使用用户当前明确提供的路径，先只读检查目录是否存在且可访问；路径无效时说明问题，不静默换到其他目录。
- 用户明确要求初始化后，只把 `assets/vault-template/` 中缺失的文件复制到该 Vault 根目录；保留已有文件和 `.obsidian/` 配置，遇到文件与目录冲突时报告具体路径。
- 对本次新建的 `VAULT_INDEX.md`，把根目录占位说明替换为实际使用的完整路径；已有索引不因初始化而覆盖。
- 后续会话依次考虑：用户当前明确路径、当前项目已确认且可访问的路径、`CODEBRAIN_HOME`、已存在的 `~/CODEBRAIN`。无明确选择且候选路径冲突时询问用户。
- 不声称聊天中的路径会自动永久保存；提醒用户后续再次提供路径，或自行配置 `CODEBRAIN_HOME`。告知路径不授权修改系统环境变量、全局协议或创建符号链接。
- 只有用户明确选择不用 Vault 时，才退回项目内 `docs/codex/<task-slug>/`；不能用该目录替代首次 Vault 初始化要求。

本 skill 安装在 `~/.codex/skills/codebrain-memory` 时是全局可见的；但它不是后台服务，不会在 Codex 未运行时监听文件系统。自动触发依赖 skill metadata、全局 `AGENTS.md` 和当前会话的任务语义。

## 语言规则

- 面向用户的回复、写入 CODEBRAIN / Obsidian vault 的标题、字段名和正文必须使用简体中文。
- 只有文件名、路径、命令、代码标识符、API 名称、固定 skill/plugin 名称、外部错误原文和日志原文可以保留英文。
- 阶段日志、交接文档、任务、决策和经验的固定字段使用：`目标`、`读取上下文`、`决策`、`涉及文件`、`验证`、`下一步`、`风险`。
- 引用英文资料时先用简体中文总结，只在需要精确复现错误或命令时保留原文。

## 运行规则

- 把本 skill 当作工作流协调器，而不是自动化授权。
- 只能使用当前会话中真实可见、已安装、可调用的 tools、skills、plugins、connectors。
- 不要声称 hook、loop agent、GitHub 访问、部署访问或无人值守自动化已存在，除非它们确实可调用。
- Codex 负责维护项目核心状态。其他 AI 可以把原始材料投递到收件箱，但不应直接更新决策、经验或交接状态。
- 未经用户明确批准，不要删除、迁移、重写或重组 vault。
- 不要把 secrets、auth tokens、billing 数据、生产凭据、PII 或私钥写入 CODEBRAIN。

人类放行边界始终保留给用户：目标选择、风险接受、合并、部署、发布、回滚、生产数据、权限边界和 L3 无人值守自动化。

## 资源地图

只读取当前任务需要的 reference：

- `references/vault-structure.md`：vault 布局、项目核心文件、读取顺序、双链规则。
- `references/workflows.md`：会话开始、phase 结束、L1/L2/L3 Loop SOP、写入边界。
- `references/proposal-review.md`：技术方案评估的第一性原理关卡和对抗式审查关卡模板。
- `references/distribution.md`：安装、分发、路径迁移、未来 skill 拆分规则。

创建新 vault 或补齐项目记忆结构时，使用 `assets/vault-template/`。

## 工作流决策树

1. 需要初始化或修复 vault 结构？
   - 读取 `references/vault-structure.md`。
   - 复制或镜像 `assets/vault-template/`。
   - 检查用户已新建并提供完整路径的 Vault，按首次初始化规则补齐模板。

2. 开始或恢复项目工作？
   - 解析 vault root。
   - 读取 `VAULT_INDEX.md`。
   - 读取项目的 `PROJECT_INDEX.md`、`HANDOFF.md`、`TASKS.md` 和最近相关的 `PHASE_LOG.md`。
   - 只读取这些文档显式链接的代码或文档，除非索引已经过期。

3. 完成一个 phase、上下文窗口或长任务？
   - 用简明证据更新项目 `PHASE_LOG.md`。
   - 用当前状态、阻塞、下一步和风险更新 `HANDOFF.md`。
   - 只在任务状态真实变化时更新 `TASKS.md`。

4. 评估方案或高风险改动？
   - 读取 `references/proposal-review.md`。
   - 执行第一性原理关卡和对抗式审查关卡。
   - 输出推荐方案、更简单方案、被拒绝方案、取舍、失败模式和验证计划。

5. 运行 Loop Engineering？
   - L1 只报告：只检查、报告或更新状态，不改业务代码。
   - L2 协助修复：需要明确用户目标、最小范围、验证证据和独立验证者视角。
   - L3 无人值守：默认拒绝，除非用户明确给出预算、权限、禁止清单、回滚计划、日志和人类放行点。

## Vault 读取顺序

按这个顺序读取，避免全 vault 扫描：

1. `VAULT_INDEX.md`
2. `01_Projects/<project-slug>/PROJECT_INDEX.md`
3. `01_Projects/<project-slug>/HANDOFF.md`
4. `01_Projects/<project-slug>/TASKS.md`
5. `01_Projects/<project-slug>/PHASE_LOG.md` 中最近相关的条目
6. 以上文档显式链接的文件

如果索引缺失，先创建或修复最小可用索引，再继续。

## 写入策略

Codex 可以更新：

- `TASKS.md`：任务状态和优先级变化。
- `PHASE_LOG.md`：只追加的阶段摘要。
- `HANDOFF.md`：当前工作状态。
- `DECISIONS.md`：只写入已确认的决策。
- `LESSONS.md`：只写入可复用、已验证的经验。

其他 AI 的输出应放入：

- `00_Inbox/raw/`
- `00_Inbox/triaged/`
- `01_Projects/<project-slug>/_inbox/`

只有当收件箱材料经过验证、关联到项目，并且对未来工作有用时，才提升到核心状态文件。

## 输出契约

使用本 skill 时，最终报告必须说明：

- 使用的 vault 根目录。
- 使用或创建的项目 slug。
- 读取了哪些文件。
- 修改了哪些文件。
- 做了哪些验证。
- 剩余风险或假设。
