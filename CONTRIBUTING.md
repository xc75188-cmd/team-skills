# 贡献指南

感谢你为团队 Skills Registry 做贡献！请遵循以下流程。

## 提交流程

```
1. 创建分支    git checkout -b feat/add-xxx-skill
2. 编写内容    按模板填写 Skill 或 Prompt
3. 本地检查    确保文件结构完整
4. 提交 PR     推送分支并创建 Pull Request
5. CI 检查     等待自动检查通过
6. 人工审核    至少 1 位成员 approve
7. 合并        Squash merge 到 main
```

## 新增 Skill

1. 复制对应模板：
   ```bash
   # 新增 Skill（放到对应分类下）
   cp -r templates/skill-template/ skills/code/你的skill名/

   # 新增 Prompt（放到对应分类下）
   cp -r templates/prompt-template/ prompts/writing/你的prompt名/
   ```
3. 按模板内容填写
4. 提交 PR

## 修改已有 Skill

1. 创建分支
2. 修改内容
3. 在 PR 描述中说明改了什么、为什么改
4. 提交 PR

## 分支命名规范

| 类型 | 格式 | 示例 |
|------|------|------|
| 新增 | `feat/add-xxx` | `feat/add-code-review-skill` |
| 修改 | `fix/update-xxx` | `fix/update-meeting-summary` |
| 文档 | `docs/update-xxx` | `docs/update-contributing` |
| 删除 | `chore/remove-xxx` | `chore/remove-deprecated-skill` |

## PR 描述模板

提交 PR 时请包含以下信息：

- **类型**：新增 / 修改 / 删除
- **影响范围**：涉及哪些 Skill 或 Prompt
- **变更说明**：做了什么、为什么做
- **测试**：是否实际使用过该 Skill/Prompt，效果如何

## Skill 质量要求

提交的 Skill / Prompt 需要满足：

- **有实际使用场景**：不要提交"可能有用"但从没用过的内容
- **SKILL.md 或 prompt.md 说明清晰**：其他人能看懂怎么用
- **不包含敏感信息**：API Key、Token、密码、内部数据库地址等
- **命名规范**：目录名用小写字母和 `-`，如 `code-review`

## 审核标准

Reviewer 请关注：

1. **实用性**：是否解决真实问题
2. **可复用性**：其他成员能否直接使用
3. **安全性**：是否包含敏感信息或危险操作
4. **重复性**：仓库中是否已有类似内容
5. **文档完整性**：说明是否足够清晰

## 涉及脚本的特殊规则

如果 Skill 包含 shell 脚本、数据访问逻辑、或调用外部 API，需要：

- 至少 **2 人** review
- 在 PR 中明确说明脚本的作用和权限需求
