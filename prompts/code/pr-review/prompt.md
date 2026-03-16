---
name: pr-review
description: 标准化的 PR 审查 Prompt，用于快速审查 Pull Request
author: gavin-yang
tags: [engineering, code-review, pr]
created: 2026-03-16
---

# PR Review Prompt

## 用途

在审查 Pull Request 时使用，帮助快速识别代码问题并生成结构化的 review 意见。

## 适用工具

ChatGPT、Claude、Copilot Chat 等支持对话的 AI 工具。

## Prompt 内容

```
请审查以下 Pull Request 的代码变更。

PR 信息：
- 标题：{pr_title}
- 描述：{pr_description}

代码变更：
{code_diff}

请按以下格式输出审查意见：

1. 总体评价（1-2 句话）
2. 问题清单（按严重程度排列）：
   - 🔴 阻塞问题：必须修复才能合并
   - 🟡 建议修改：不影响合并但建议改进
   - 🟢 小建议：代码风格等可选优化
3. 每个问题请说明：
   - 文件和行号
   - 问题描述
   - 建议的修改方式
4. 结论：approve / request changes / comment
```

## 变量说明

| 变量 | 说明 | 示例 |
|------|------|------|
| `{pr_title}` | PR 标题 | `fix: 修复用户登录超时问题` |
| `{pr_description}` | PR 描述 | `修复了 token 刷新逻辑的竞态条件` |
| `{code_diff}` | 代码 diff 内容 | git diff 输出 |

## 使用示例

### 输入

```
PR 信息：
- 标题：feat: 添加用户导出功能
- 描述：支持将用户列表导出为 CSV 格式

代码变更：
+ def export_users(query):
+     users = db.query(query)
+     return users.to_csv()
```

### 输出

```
总体评价：功能简洁，但存在 SQL 注入风险需要修复。

🔴 阻塞问题：
- export_users 函数直接接受 query 参数执行数据库查询，
  存在 SQL 注入风险。建议使用参数化查询或 ORM 过滤。

结论：request changes
```

## 使用技巧

- 提供完整的 diff 上下文效果更好（包含修改前后的代码）
- 如果有项目的编码规范文档，一并提供可以得到更准确的建议
