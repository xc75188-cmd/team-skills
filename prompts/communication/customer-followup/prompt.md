---
name: customer-followup
description: 根据客户沟通记录生成个性化的跟进邮件
author: gavin-yang
tags: [marketing, sales, email, followup]
created: 2026-03-16
---

# 客户跟进邮件 Prompt

## 用途

根据与客户的沟通记录（会议纪要、聊天记录等），生成个性化的跟进邮件草稿。

## 适用工具

ChatGPT、Claude 等。

## Prompt 内容

```
请根据以下客户沟通记录，生成一封跟进邮件。

客户信息：
- 公司：{company}
- 联系人：{contact_name}
- 职位：{contact_title}

沟通记录：
{meeting_notes}

要求：
- 语气专业友好，不要过于正式也不要太随意
- 邮件长度控制在 200 字以内
- 必须提及沟通中讨论的具体内容（而不是泛泛而谈）
- 明确下一步行动和时间
- 使用 {language} 撰写
```

## 变量说明

| 变量 | 说明 | 示例 |
|------|------|------|
| `{company}` | 客户公司名 | `Acme Corp` |
| `{contact_name}` | 联系人姓名 | `张经理` |
| `{contact_title}` | 联系人职位 | `技术总监` |
| `{meeting_notes}` | 沟通记录摘要 | 会议纪要或聊天记录 |
| `{language}` | 邮件语言 | `中文` / `English` |

## 使用技巧

- 提供越具体的沟通记录，生成的邮件越个性化
- 如果有多次沟通，提供最近一次的即可
- 生成后务必人工检查，确保内容准确
