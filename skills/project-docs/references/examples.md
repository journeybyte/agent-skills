# 输出示例

用于校准文档结构与产物粒度，按需读取，不随主流程常驻上下文。Step 编号见 `SKILL.md` 的 Prompt Template。Example 1–3 只展示产物结构，省略交付摘要；摘要完整格式见 Example 4、6、8–11。

## Example 1: Vue 前端项目

**Input:** 初始化项目文档
**Output:**
- AGENTS.md（行为准则 + 场景导航 + 常用命令）
- docs/PROJECT.md（技术栈、目录结构）
- docs/COMPONENT.md（改组件时需单独查阅组件规范）
- docs/API_CONVENTIONS.md（改接口时需单独查阅请求封装和错误处理约定）

**AGENTS.md 内容基准:**
- 行为准则：Step 4 四节原文
- 技术栈概览：框架、语言、包管理器、关键依赖，各一行
- 场景导航表：场景 | 何时查阅 | 文档路径
- 常用命令：dev / build / test / lint
- 测试方式：测试命令 + 关键测试目录；团队用 PR 流程时补分支/提交要求

## Example 2: 单文件 Node.js CLI 工具

**Input:** 请帮我创建这个项目的 AI 开发文档
**Output:**
- AGENTS.md（行为准则 + 场景导航 + 常用命令）
- docs/PROJECT.md（技术栈、目录结构 + CLI 参数说明合并于此，因内容简短）
- （项目简单，领域信息不足独立文档价值，不生成额外子文档）

## Example 3: 前后端分离全栈项目

**Input:** 设置项目开发文档
**Output:**
- AGENTS.md（行为准则 + 场景导航 + 常用命令）
- docs/PROJECT.md（技术栈、目录结构、架构模式）
- docs/API_CONVENTIONS.md（改接口时需单独查阅接口约定）
- docs/ARCHITECTURE.md（跨模块改动时需单独查阅架构决策）
- docs/DATA_MODEL.md（改数据结构时需单独查阅模型定义）

## Example 4: 架构变更后同步文档（更新模式）

**Context:** 项目已有上例的全套文档，数据层原有 8 个表（已满足 `DATA_MODEL.md` 的 ≥3 阈值），本次扩展到 12 个表，并新增独立的数据校验模块。

**Input:** 项目结构变了，同步更新一下文档
**Output:**
- 变更差异清单（数据模型扩展、新增校验模块）
- AGENTS.md `[修订]`：场景导航表新增"数据校验"入口，其余章节未动
- docs/DATA_MODEL.md `[修订]`：表清单由 8 个扩为 12 个，原有格式与说明保留
- docs/VALIDATION.md `[新增]`：校验模块命中固定映射表，独立成文并加入导航
- docs/PROJECT.md `[未动]`：只列路径，不重复输出
- docs/API_CONVENTIONS.md、docs/ARCHITECTURE.md `[未动]`：只列路径，不重复输出

**交付摘要（按 SKILL.md"反馈格式"6 项模板）：**
```
1. 模式与档位：更新；L1；触发依据：用户明确要求同步文档；未生成升级项：无
2. 文件状态：
   - docs/VALIDATION.md [新增] — 校验模块独立成文
   - AGENTS.md [修订] — 导航表新增入口
   - docs/DATA_MODEL.md [修订] — 表清单扩充
   - docs/API_CONVENTIONS.md [未动] — 只列路径
   - docs/ARCHITECTURE.md [未动] — 只列路径
   - docs/PROJECT.md [未动] — 只列路径
3. 变更依据：变更差异清单 2 项（数据模型扩展、新增校验模块）
4. 重写说明：无
5. 降级与后续：无
6. 问题清单：无
```

## Example 5: 单独编写 README

**Input:** 帮我给这个项目写一份 README
**Output:**
- 单产物模式：只生成 README.md
- 不创建 AGENTS.md 与 docs/；定位无法从代码确认时先向用户提问

**README.md 内容基准:**
- 项目名 + 一句话定位
- 前置要求：运行时与包管理器版本
- 快速开始：安装 → 配置（环境变量）→ 运行
- 常用命令：dev / build / test / lint
- 目录结构（简短）
- 文档入口：AGENTS.md / docs/ 存在时指向，不存在时省略并列入问题清单，不写死链接
- 贡献与许可（缺失时注明未提供）

**交付摘要（单产物模式，仅第 2、6 项）：**
```
2. 文件状态：
   - README.md [新增] — 按内容基准生成，定位已从配置文件确认
6. 问题清单：无
```

## Example 6: 文档初始化并附带 README / API 参考

**Context:** 沿用 Example 1 的 Vue 项目，用户额外要求 README 与接口文档。
**Input:** 初始化项目文档，顺便补一份 README 和接口文档
**Output:**
- 基线文档与动态文档（按前例规则）
- README.md（按 Example 5 内容基准）
- docs/API_REFERENCE.md（按下方内容基准）
- 无法从代码确认的定位或接口列入问题清单，不编造

**docs/API_REFERENCE.md 内容基准:**
- 契约来源：OpenAPI 文件路径 + 版本，或路由定义位置
- 概述：base URL、API 版本、认证方式、Content-Type
- 错误模型：统一错误结构 + 常见状态码
- 接口条目：METHOD /path、参数表（path/query/body/header）、请求示例、响应示例、错误码
- 分页/限流/幂等：仅在接口定义确认时写

**交付摘要（初始化，6 项）：**
```
1. 模式与档位：初始化；L1；触发依据：无团队/对外信号；未生成升级项：CONTRIBUTING、SECURITY、CHANGELOG
2. 文件状态：
   - AGENTS.md [新增] — 主索引
   - docs/PROJECT.md [新增] — 项目概览
   - docs/COMPONENT.md [新增] — 组件规范
   - docs/API_CONVENTIONS.md [新增] — 请求与错误约定
   - README.md [新增] — 用户要求
   - docs/API_REFERENCE.md [新增] — 用户要求
3. 变更依据：无
4. 重写说明：无
5. 降级与后续：无
6. 问题清单：无
```

## Example 7: 不触发的请求

**Input:** 帮我润色一下这段产品介绍文案
**Output:** 不激活本技能；与项目结构无关的纯文字润色不在范围内。

## Example 8: 开源库（L3）

**Context:** package.json 非 private，已有 LICENSE、CI、SECURITY.md、CHANGELOG.md 与发布流水线，用户说明项目开源。
**Input:** 初始化项目文档
**Output:**
- 档位 L3（对外），触发信号：用户说明开源 + 已有安全/变更记录 + 发布配置
- AGENTS.md、docs/PROJECT.md、docs/API_CONVENTIONS.md
- CONTRIBUTING.md、SECURITY.md、CHANGELOG.md
- README.md（安装/用法/兼容矩阵）
- docs/API_REFERENCE.md（公开 API 深度）

**交付摘要（初始化，6 项）：**
```
1. 模式与档位：初始化；L3；触发依据：用户说明开源 + 已有 SECURITY/CHANGELOG/发布配置；未生成升级项：无
2. 文件状态：
   - AGENTS.md [新增] — 主索引
   - CONTRIBUTING.md [新增] — 贡献流程
   - README.md [新增] — 安装/用法/兼容矩阵
   - docs/PROJECT.md [新增] — 项目概览
   - docs/API_CONVENTIONS.md [新增] — 请求与错误约定
   - docs/API_REFERENCE.md [新增] — 公开 API 深度
   - CHANGELOG.md [修订] — 补齐现有变更记录格式
   - SECURITY.md [修订] — 补齐支持的版本与报告渠道
3. 变更依据：无
4. 重写说明：无
5. 降级与后续：无
6. 问题清单：无
```

## Example 9: 团队仓库（L2）

**Context:** 仓库已有 CONTRIBUTING.md、PR 模板和 CI，满足至少两项团队信号；未开源。
**Input:** 初始化项目文档
**Output:**
- 档位 L2（团队），触发信号：CONTRIBUTING + PR 模板（≥2 项团队信号）
- AGENTS.md、docs/PROJECT.md
- CONTRIBUTING.md [修订]（补充环境准备与测试要求）
- 不生成 README、SECURITY、CHANGELOG（未命中 L3）

**交付摘要（初始化，6 项）：**
```
1. 模式与档位：初始化；L2；触发依据：已有 CONTRIBUTING 与 PR 模板；未生成升级项：README、SECURITY、CHANGELOG
2. 文件状态：
   - AGENTS.md [新增] — 主索引，含代码风格与安全边界
   - docs/PROJECT.md [新增] — 项目概览
   - CONTRIBUTING.md [修订] — 补充环境准备与测试要求
3. 变更依据：无
4. 重写说明：无
5. 降级与后续：无
6. 问题清单：无
```

## Example 10: 初始化请求降级为更新（已有 AGENTS.md）

**Context:** 项目已有 Example 1 生成的全套文档（AGENTS.md、docs/PROJECT.md、docs/COMPONENT.md、docs/API_CONVENTIONS.md）。用户要求"初始化项目文档"，但未含"从零重建/覆盖/重新生成"等显式重写词。用户未指出具体变更点。

**Input:** 初始化项目文档
**Output:**
- 判定为更新模式：已有 AGENTS.md 且无显式重建词，"初始化"类请求默认降级按更新处理；交付摘要第 1 项注明
- 变更点未确认：不向用户提问，以当前实际结构为准逐项对比现有文档（命中"更新模式下变更点无法确认"边界）
- 本次对比确认 2 项差异：package.json 新增 1 个依赖、src/utils 新增目录
- 只修订受影响章节，未动文件只列路径

**交付摘要（更新，6 项）：**
```
1. 模式与档位：更新（用户要求初始化，已有 AGENTS.md，未显式要求重建，默认按更新处理）；L1；触发依据：用户"初始化项目文档"请求 + 已有 AGENTS.md；未生成升级项：无
2. 文件状态：
   - AGENTS.md [修订] — 技术栈概览补新增依赖
   - docs/PROJECT.md [修订] — 目录结构同步 src/utils
   - docs/COMPONENT.md [未动] — 只列路径
   - docs/API_CONVENTIONS.md [未动] — 只列路径
3. 变更依据：变更差异清单 2 项（新增依赖、新增 src/utils 目录）
4. 重写说明：无
5. 降级与后续：无
6. 问题清单：无
```

## Example 11: 重写式初始化（显式要求从零重建）

**Context:** 沿用 Example 1 的 Vue 项目。项目经过大量重构：目录大改、组件目录移除，现有文档与实际严重不符。用户明确要求重建。旧 docs/API_CONVENTIONS.md 中有一条手写规范（"接口错误码统一走 4xxx 段"），代码中无法直接确认该约定仍有效。

**Input:** 文档太乱了，从零重建一套吧
**Output:**
- 判定为初始化模式（重写）：已含"从零重建"显式重写词
- 先读取全部现有文档履行保真义务：手写的 4xxx 错误码规范无法从代码确认，向用户确认仍适用后迁移进新 docs/API_CONVENTIONS.md，标注来源为旧文档
- 整体重写 AGENTS.md、docs/PROJECT.md、docs/API_CONVENTIONS.md，不以旧文档为基线，重写文件标 `[重写]`
- docs/COMPONENT.md 对应的组件目录已移除、领域不存在 → 删除并移除导航条目

**交付摘要（初始化（重写），6 项）：**
```
1. 模式与档位：初始化（重写）；L1；触发依据：用户显式要求"从零重建"；未生成升级项：无
2. 文件状态：
   - AGENTS.md [重写] — 按当前结构整体重新生成
   - docs/PROJECT.md [重写] — 目录大改后重新生成
   - docs/API_CONVENTIONS.md [重写] — 重新生成，迁移旧文档手写的错误码规范
   - docs/COMPONENT.md [已删除] — 组件目录已移除，领域不再存在
3. 变更依据：无
4. 重写说明：AGENTS.md、docs/PROJECT.md、docs/API_CONVENTIONS.md — 大量目录/模块已变且用户显式要求从零重建
5. 降级与后续：无
6. 问题清单：无
```
