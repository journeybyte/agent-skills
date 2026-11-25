# 仓库画像与文档档位

先判画像，再按档位定文档清单。默认最低档，命中信号才升级；用户指定档位优先。信号冲突或无法确认时按 L1，并在交付摘要说明可升级项。

## 1. 仓库类型

| 类型 | 判定信号（按优先级） | 文档差异 |
|---|---|---|
| CLI | package.json `bin`，或单一可执行入口 | README 补命令、参数与示例 |
| 库/SDK | `main` / `exports` / `types`，无 `bin` | README 补安装、用法示例、兼容矩阵；API 参考按导出面 |
| 应用/服务 | `scripts.start`、框架依赖、Dockerfile 等部署配置 | README 补环境变量、部署与访问方式 |
| monorepo | workspaces / pnpm-workspace / lerna / nx / turbo | 根 AGENTS.md + 按包边界拆分子文档；包内文档就近存放 |

无配置文件时按目录与入口判断；仍无法确认时向用户提问，不猜。

## 2. 文档档位

| 档位 | 触发信号 | 文档清单 |
|---|---|---|
| L1 精简（默认） | 无团队/对外信号 | AGENTS.md + docs/PROJECT.md + 按复杂度生成的领域文档 |
| L2 团队 | 以下至少两项：CONTRIBUTING、CODEOWNERS、PR 模板、CI 工作流 | L1 + CONTRIBUTING.md；AGENTS 补代码风格、测试策略、安全边界；领域文档补示例与检查清单 |
| L3 对外 | 用户明确开源/公开 API，或同时存在 SECURITY.md、CHANGELOG.md、发布配置 | L2 + README.md + SECURITY.md + CHANGELOG.md + docs/API_REFERENCE.md（有 API 时） |

- 升级只补缺失项，不重写已有文档；用户可指定或降级档位。
- 交付时列出档位、触发信号、未生成的升级项。

## 3. 档位文档要点

- CONTRIBUTING.md：环境准备、分支与提交规范、评审与测试要求、发布流程（有定义时）。
- SECURITY.md：支持的版本、漏洞报告渠道、响应时限；不写无来源的承诺。
- CHANGELOG.md：Keep a Changelog 结构，按版本倒序；未发布变更放 Unreleased。
- README.md / API_REFERENCE.md：内容规则见 SKILL.md"扩展产物（可选）"。

## 4. README 类型差异

- 库：安装、最小用法示例、导出面、兼容矩阵、版本策略。
- 应用：部署方式、环境变量、访问入口、界面截图（有界面时）。
- CLI：安装、命令清单、参数与示例、退出码（有定义时）。
共用骨架见 SKILL.md"扩展产物（可选）"。

## 5. 公开 API 的额外要求

内部 API 按基础参考生成；公开 API 再加版本与弃用策略、错误码表、SDK/OpenAPI 链接、限流/幂等（有定义时）。

## 6. 不默认生成

ADR、docs 索引、CODE_OF_CONDUCT、按类型拆分的 README 模板：用户明确要求时再补。
