# Changelog

本文件记录 `project-docs` 技能的版本变更，格式参考 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/)。

## [2026-11-26] - e2ae0cb

### 新增

- 新增 `references/feedback.md`：统一问题清单、6 项交付摘要、状态前缀（`[未动]` / `[修订]` / `[新增]` / `[已删除]`），`[降级]` 作为注记。
- Step 3 新增固定映射表与阈值：组件复用、接口约定、跨模块架构、数据模型（表 ≥3）、数据校验（规则 ≥3）。
- 新增动态文档命名白名单与 `UPPER_SNAKE_CASE.md` 规则；`api-conventions.md` 统一为 `API_CONVENTIONS.md`。
- 新增 monorepo 包边界拆分规则：包级概览写 `<package>/docs/PROJECT.md`，根导航收录各包文档。
- 新增单产物示例与 L2 团队仓库示例，覆盖 README、L2、L3 组合产物。

### 变更

- 反馈格式从 `SKILL.md` 下沉到 `references/feedback.md`，正文按需加载。
- `AGENTS.md` 改为固定骨架；80–120 行（L2 可到 140 行）改为参考值，不再作为硬性通过条件。
- README 上限由 100 行调整为 120 行，明确“必需章节优先，超出压缩目录与技术栈细节”。
- `description` 从 322 字符压缩到 148 字符，降低常驻上下文占用。
- 初始化/更新/单产物三种模式的交付摘要与状态前缀统一；单产物只输出第 2、6 项。
- 用户指定表外领域可按 `UPPER_SNAKE_CASE.md` 新增，不再强制并入 `docs/PROJECT.md`。
- 示例补齐交付摘要：Example 4/6/8/9 分别覆盖更新、初始化、L3、L2 场景。

### 修复

- 修正删除/重命名权限：覆盖 monorepo 包内 `docs/`；删除前确定待删清单，交付摘要说明结果。
- 修正“第 2、3 行”为“第 2、3 项”；`[降级]` 不再参与文件状态分组。
- 修正 L3 示例中已存在的 `SECURITY.md` / `CHANGELOG.md` 被误标为 `[新增]` 的问题。
- 修正命名白名单“不得超出”与用户指定新增领域规则的冲突。
- 统一 `docs/PROJECT.md` 路径写法与生成文档命名大小写。

### 兼容性

- 技能名与目录保持 `project-docs`。
- 更新模式遇到历史小写/连字符文件名（如 `component.md`）时沿用原名，不改名、不新建。
- 无破坏性接口变更；已安装用户重新拉取技能即可。

### 验证

- frontmatter `name` 与目录一致；`references/` 下 3 个文件均存在。
- 代码围栏成对；0 lint 错误。
- 5 个交付摘要块校验通过（4 个完整 6 项，1 个单产物 2/6 项）。
- 尚未在真实仓库执行 L1/L2/L3/monorepo 全流程测试。
