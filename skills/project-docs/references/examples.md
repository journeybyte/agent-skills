# 输出示例

用于校准文档结构与产物粒度，按需读取，不随主流程常驻上下文。Step 编号见 `SKILL.md` 的 Prompt Template。

## Example 1: Vue 前端项目

**Input:** 初始化项目文档
**Output:**
- AGENTS.md（行为准则 + 场景导航 + 常用命令）
- docs/PROJECT.md（技术栈、目录结构）
- docs/COMPONENT.md（改组件时需单独查阅组件规范）
- docs/api-conventions.md（改接口时需单独查阅请求封装和错误处理约定）

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
- docs/api-conventions.md（改接口时需单独查阅接口约定）
- docs/ARCHITECTURE.md（跨模块改动时需单独查阅架构决策）
- docs/DATA_MODEL.md（改数据结构时需单独查阅模型定义）

## Example 4: 架构变更后同步文档（更新模式）

**Context:** 项目已有上例的全套文档，本次把数据层从 2 个表扩展到 8 个表，并新增独立的数据校验模块。

**Input:** 项目结构变了，同步更新一下文档
**Output:**
- 变更差异清单（数据模型扩展、新增校验模块）
- AGENTS.md: 修订（场景导航表新增"数据校验"入口，其余章节未动）
- docs/DATA_MODEL.md: 修订（表清单由 2 个扩为 8 个，原有格式与说明保留）
- docs/VALIDATION.md: 新增（校验模块复杂度达标，独立成文并加入导航）
- docs/PROJECT.md: 未动（只列路径，不重复输出）
- docs/api-conventions.md、docs/ARCHITECTURE.md: 未动（只列路径，不重复输出）

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
- 文档入口：AGENTS.md / docs/
- 贡献与许可（缺失时注明未提供）

## Example 6: 文档初始化并附带 README / API 参考

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

## Example 7: 不触发的请求

**Input:** 帮我润色一下这段产品介绍文案
**Output:** 不激活本技能；与项目结构无关的纯文字润色不在范围内。

## Example 8: 开源库（L3）

**Context:** package.json 非 private，已有 LICENSE、CI、SECURITY.md、CHANGELOG.md 与发布流水线，用户说明项目开源。
**Input:** 初始化项目文档
**Output:**
- 档位 L3（对外），触发信号：用户说明开源 + 已有安全/变更记录 + 发布配置
- AGENTS.md、docs/PROJECT.md、docs/api-conventions.md
- CONTRIBUTING.md、SECURITY.md、CHANGELOG.md
- README.md（安装/用法/兼容矩阵）
- docs/API_REFERENCE.md（公开 API 深度）
