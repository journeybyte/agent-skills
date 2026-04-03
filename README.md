# agent-skills

AI Agent 技能集合，为智能助手提供可扩展的专业能力。

## 📁 项目结构

```
agent-skills/
├── skills/                      # 技能目录
│   └── project-doc-init/       # 项目文档初始化技能
│       └── SKILL.md            # 技能定义文件
├── LICENSE                      # MIT许可证
└── README.md                    # 项目说明文档
```

## 🛠️ 可用技能

### project-doc-init

**通用项目 AI 文档初始化技能**

通过分析项目特点，自动生成一套 AI 友好的文档体系，包括场景化导航、最佳实践规范和代码模板。适用于任何技术栈的项目。

**触发词：**
- 初始化项目文档
- 创建 AI 开发文档
- 初始化 AI 文档
- 设置项目文档结构
- 项目文档初始化
- initialize project documentation
- create project docs
- AI documentation setup

**功能特点：**
- 自动识别技术栈（Vue/React/Node等）
- 生成 CLAUDE.md 主索引文档
- 创建 docs/ 目录结构
- 提供场景化导航表
- 包含代码模板和规范说明

## 🚀 使用方法

### 在 Trae IDE 中使用

1. 打开 Trae IDE
2. 在对话中激活技能，例如：
   ```
   初始化项目文档
   ```
3. 技能将自动分析当前项目
4. 生成完整的文档体系

### 本地开发

如果需要修改或扩展技能：

1. 编辑对应技能目录下的 `SKILL.md` 文件
2. 确保遵循技能规范（见下文）
3. 测试技能功能
4. 提交更改

## 📖 技能规范

所有技能必须符合以下规范：

### 必需结构

```
---
name: <技能名称>           # 必须与目录名一致
description: <简短描述>    # 说明技能用途
---

# <技能标题>

## Description
详细的功能描述

## Triggers
触发条件列表

## Usage
使用说明

## Instructions
详细执行步骤

## Output Format
输出格式说明

## Examples
使用示例
```

### 命名规范

- 目录名：`kebab-case`（如 `project-doc-init`）
- YAML name：与目录名一致
- 文件名：必须为 `SKILL.md`

### 内容要求

1. **清晰的范围定义** - 明确技能的功能边界
2. **具体的触发条件** - 包含中英文触发词
3. **详细的执行步骤** - Step-by-step 说明
4. **格式化的输出** - 提供输出模板
5. **实用的示例** - 展示典型使用场景

## 📝 添加新技能

1. 在 `skills/` 目录下创建新目录
2. 编写 `SKILL.md` 文件
3. 包含完整的 YAML frontmatter
4. 遵循上述规范结构
5. 更新本 README 的技能列表

## 🔧 工具链

- **包管理**: pnpm
- **许可证**: MIT License
- **版权**: Copyright (c) 2026 Zenith·Journey

## 📄 许可证

本项目采用 MIT License - 详见 [LICENSE](LICENSE) 文件

---