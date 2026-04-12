---
title: Claude Code - Plugin与Skill安装记录
date: 2026-04-12
tags:
  - claude-code
  - skill
  - plugin
---

# Claude Code Plugin 与 Skill 安装记录

> [!info] 对话时间
> 2026-04-12

## Skill 基础知识

### Skill 安装位置

| 作用域 | 路径 |
|--------|------|
| 个人（全局） | `~/.claude/skills/<skill-name>/SKILL.md` |
| 项目级 | `.claude/skills/<skill-name>/SKILL.md` |

**SKILL.md 基本格式：**

```markdown
---
name: my-skill
description: 描述这个 skill 的用途
---

你的指令内容...
```

调用方式：`/my-skill` 或由 Claude 根据 description 自动触发。

---

## 已安装的 Plugin

### 1. frontend-design

```
/plugin install frontend-design@claude-plugins-official
```

**功能：** 创建高质量、生产级前端界面，避免 AI 生成的通用风格。

---

### 2. superpowers

```
/plugin install superpowers@claude-plugins-official
```

**功能：** 专业软件工程最佳实践工作流集合。

| Skill | 用途 |
|-------|------|
| `superpowers:brainstorming` | 创意/功能开发前探索需求 |
| `superpowers:writing-plans` | 制定多步骤实施计划 |
| `superpowers:executing-plans` | 执行已有实施计划 |
| `superpowers:test-driven-development` | 先写测试再写实现 |
| `superpowers:systematic-debugging` | 系统性排查 bug |
| `superpowers:verification-before-completion` | 完成前运行验证命令 |
| `superpowers:requesting-code-review` | 请求代码审查 |
| `superpowers:receiving-code-review` | 严谨评估审查意见 |
| `superpowers:dispatching-parallel-agents` | 并行派发多个 agent |
| `superpowers:using-git-worktrees` | 创建隔离 git worktree |
| `superpowers:finishing-a-development-branch` | 完成开发分支收尾 |
| `superpowers:writing-skills` | 创建/编辑 skill |

---

### 3. skill-creator

```
/plugin install skill-creator@claude-plugins-official
```

**功能：** 从零创建 skill、更新优化现有 skill、运行 skill 评估测试。

---

### 4. obsidian

```
/plugin marketplace add kepano/obsidian-skills
/plugin install obsidian@obsidian-skills
```

**来源：** [[https://github.com/anthropics/claude-plugins-official/tree/main/plugins/skill-creator]]

**包含的 Skill：**

| Skill | 功能 |
|-------|------|
| `obsidian:obsidian-markdown` | 创建/编辑 Obsidian 风格 Markdown |
| `obsidian:json-canvas` | 创建/编辑 Canvas 画布文件 |
| `obsidian:defuddle` | 从网页提取干净 Markdown 内容 |
| `obsidian:obsidian-bases` | 创建/编辑 Obsidian Bases 数据库视图 |
| `obsidian:obsidian-cli` | 通过 CLI 与 Obsidian 库交互 |

> [!warning] 注意
> `obsidian:obsidian-cli` 需要官方 Obsidian CLI 工具支持（`obsidian` 命令），目前 Obsidian 1.10.3 设置中未找到相关选项，暂无法使用该 skill。
> 
> 已安装的 `obsidian-cli`（Yakitrak 版，命令为 `obsidian-cli`）为第三方工具，与官方 CLI 不同。

**Vault 信息：**
- 默认 Vault 名称：`Documents`
- 路径：`/Users/yangxiaomao/Library/Mobile Documents/iCloud~md~obsidian/Documents`
