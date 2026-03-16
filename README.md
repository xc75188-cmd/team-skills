# Team Skills Registry

团队 AI Agent Skills & Prompts 统一管理仓库。

## 这是什么

这个仓库集中管理团队内部使用的 AI Agent Skills 和 Prompt 模板，解决以下问题：

- Prompt 散落在 Notion、Slack、本地文件、聊天记录中，无法复用
- 不同成员重复编写类似的 Skill 和 Prompt
- 修改后无法追溯、回滚、审计
- 缺少安全审核机制

## 仓库结构

```
team-skills/
├── skills/                # Agent Skills（按用途分类）
│   ├── code/              # 编码：审查、重构、调试、测试
│   ├── writing/           # 写作：文档、报告、邮件
│   ├── research/          # 调研：竞品分析、数据分析
│   ├── automation/        # 自动化：工作流、脚本、CI/CD
│   └── communication/     # 沟通：会议纪要、消息整理
├── prompts/               # Prompt 模板（同样按用途分类）
│   ├── code/
│   ├── writing/
│   ├── research/
│   ├── automation/
│   └── communication/
├── templates/             # 新建 Skill / Prompt 的模板
│   ├── skill-template/
│   └── prompt-template/
└── .github/
    └── workflows/         # CI 自动检查
```

## 快速开始

### 使用已有的 Skill

根据你使用的 Agent 工具，将 Skill 复制或链接到对应位置：

```bash
# Claude Code
cp -r skills/communication/meeting-summary/ /你的项目/.claude/skills/

# 或创建符号链接（始终使用最新版本）
ln -s $(pwd)/skills/communication/meeting-summary/ /你的项目/.claude/skills/meeting-summary
```

其他 Agent 工具请参考各自的文档，将 Skill 目录复制到对应路径即可。

### 使用已有的 Prompt

直接打开 `prompts/` 下对应的 `.md` 文件，复制内容到你使用的 AI 工具中。

### 贡献新的 Skill 或 Prompt

请阅读 [CONTRIBUTING.md](CONTRIBUTING.md) 了解完整提交规范。

简要流程：

```bash
# 1. 克隆仓库（如果还没有）
git clone git@github.com:AgentStaff/team-skills.git
cd team-skills

# 2. 从 main 创建你的分支
git checkout main
git pull origin main
git checkout -b feat/add-你的skill名

# 3. 复制模板，编写内容
cp -r templates/skill-template/ skills/code/你的skill名/
# 编辑 skills/code/你的skill名/SKILL.md

# 4. 提交并推送
git add .
git commit -m "feat: 添加 xxx skill"
git push origin feat/add-你的skill名

# 5. 在 GitHub 上创建 Pull Request，等待 review
# PR 合并后，你的远程分支会被自动删除
```

**注意事项：**

- **禁止直接推送到 `main` 分支**，所有变更必须通过 PR 提交
- 每个 PR 需要至少 1 位成员 review 并 approve 后才能合并
- CI 会自动检查文件结构和敏感信息，请确保 CI 通过后再请求 review
- PR 合并后远程分支会自动删除，本地分支需要手动清理：`git branch -d feat/add-xxx`

## 命名规范

### 目录命名

- 全部使用**小写英文字母**，单词之间用 `-` 连接
- 不要用下划线 `_`、驼峰命名、中文或空格
- 分类目录固定为：`code`、`writing`、`research`、`automation`、`communication`

| 示例 | 是否合规 |
|------|----------|
| `code-review` | ✅ |
| `meeting-summary` | ✅ |
| `CodeReview` | ❌ 不要用驼峰 |
| `code_review` | ❌ 不要用下划线 |
| `会议总结` | ❌ 不要用中文 |

### 分支命名

| 操作 | 格式 | 示例 |
|------|------|------|
| 新增 | `feat/add-xxx` | `feat/add-code-review-skill` |
| 修改 | `fix/update-xxx` | `fix/update-meeting-summary` |
| 删除 | `chore/remove-xxx` | `chore/remove-deprecated-skill` |
| 文档 | `docs/update-xxx` | `docs/update-contributing` |

### Commit 消息

格式：`类型: 简短描述`

| 类型 | 用途 | 示例 |
|------|------|------|
| `feat` | 新增 Skill 或 Prompt | `feat: 添加 code-review skill` |
| `fix` | 修改已有内容 | `fix: 修正 meeting-summary 输出格式` |
| `docs` | 文档更新 | `docs: 更新 README 安装说明` |
| `chore` | 删除、维护、CI 配置等 | `chore: 移除废弃的 old-prompt` |

## 安全须知

- **禁止**在任何文件中包含 API Key、Token、密码等敏感信息
- Shell 脚本和涉及数据访问的 Skill 需要至少 2 人 review
- CI 会自动扫描常见的 secret 泄露模式

---

> 有问题或建议？请提 Issue 或在团队频道讨论。
