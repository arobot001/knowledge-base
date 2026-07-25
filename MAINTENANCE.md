# 维护规范与长期迭代约束

> 本文件是知识库的"宪法"，所有新增、修改、归档操作必须遵循此处定义的规则。

---

## 1. 目录结构规则

### 1.1 按类型分目录，不按主题分

```
ai/agents/         → Agent 设计、角色定义、架构方案
ai/articles/        → 文章、学习笔记、转载
ai/prompts/        → 提示词（按生成类型分子目录）
ai/skills/         → AI Skill 配置和使用说明
ai/tools/          → 工具调研、评测、推荐
inspirations/      → 灵感、想法、产品创意
posts/             → 社媒帖子收藏（X/微博等）
```

### 1.2 禁止事项

- ❌ 不要按主题建顶层目录（如 `ai/video/`、`ai/design/`）
- ❌ 不要嵌套超过 3 层（如 `ai/claude/articles/xxx.md` → 用 `ai/articles/xxx.md`）
- ❌ 不要在根目录放散文件（除 README/INDEX/MAINTENANCE）
- ❌ 不要建空目录"占位"

### 1.3 子目录规则

- `ai/prompts/` 下按生成类型分：`image-generation/`、`video-generation/`、`prompt-engineering/`
- `ai/skills/` 下按来源分：`cocoon-ai/`、`youmind/`，每个 skill 一个子目录
- `ai/tools/` 下直接放文件，不加子目录（条目少，扁平更好找）
- `posts/` 下按平台加前缀：`x-*.md`、`weibo-*.md`、`bilibili-*.md`

---

## 2. 文件命名规则

- 使用 **kebab-case**：`palmier-pro.md`、`video-editing-skills.md`
- 中文标题转拼音或英译：`OpenClaw_架构学习参考.md` → `openclaw-multi-agent-architecture.md`
- 帖子加平台前缀：`x-jackywine-design-aesthetic.md`
- 文件名 = INDEX.md 中的 slug，也是 frontmatter `related` 字段的引用值

---

## 3. Frontmatter 规范

每个 `.md` 文件**必须**以 YAML frontmatter 开头：

```yaml
---
title: "文件标题"
date: 2026-07-26
category: ai/tools
tags: [tag1, tag2, tag3]
source: web-article
author: "作者"
url: "https://..."
related: [other-file-slug, another-slug]
---
```

### 3.1 字段说明

| 字段 | 必填 | 说明 |
|------|------|------|
| `title` | ✅ | 文件标题，用引号包裹 |
| `date` | ✅ | 创建日期或最后重大更新日期，格式 YYYY-MM-DD |
| `category` | ✅ | 对应目录路径（不含 `ai/` 前缀也行，保持一致即可） |
| `tags` | ✅ | 主题标签数组，用于跨目录关联和检索 |
| `source` | ✅ | 来源类型（见下方枚举） |
| `author` | ⬜ | 原作者，如有 |
| `url` | ⬜ | 原文链接，如有 |
| `related` | ⬜ | 关联条目的 slug 列表（文件名不含 `.md`） |

### 3.2 source 枚举值

| 值 | 含义 |
|---|---|
| `custom` | 自创内容 |
| `web-article` | 网络文章 |
| `web-research` | 调研报告 |
| `github` | GitHub 项目 |
| `x-post` | X/Twitter 帖子 |
| `web` | 其他网页 |

### 3.3 tags 规则

- 小写英文为主，中文标签允许但不推荐
- 一个文件 3-8 个标签
- 标签应覆盖：**内容类型**（如 `prompt`、`research-report`）+ **主题**（如 `video-generation`、`macOS`）+ **关键技术/工具**（如 `mcp`、`seedance`）
- 避免过于细碎的标签（如 `macos-26-tahoe-only` → 用 `macOS`）

---

## 4. 新增内容流程

1. **确定目录** -> 按类型放入对应目录
2. **命名文件** -> kebab-case，见 §2
3. **写 frontmatter** -> 包含所有必填字段
4. **更新 INDEX.md** -> 在对应分类表格中添加一行
5. **设置关联** -> 在 frontmatter `related` 中填写相关条目 slug
6. **提交** -> `git add . && git commit -m "Add: 简述" && git push`

### 提交信息格式

```
Add: 新增条目标题
Update: 更新条目标题
Reorganize: 重构说明
```

---

## 5. 关联与交叉引用

### 5.1 related 字段

- 填写**文件名 slug**（不含 `.md` 扩展名）
- 双向关联：A 关联 B，B 也应关联 A
- 关联标准：**读者看完这篇，可能还想看那篇**

### 5.2 文内引用

在正文中引用其他条目时，使用相对路径链接：

```markdown
详见 [Palmier Pro 调研报告](../tools/palmier-pro.md)
```

---

## 6. 定期维护

### 6.1 月度检查（每月 1 号）

- [ ] INDEX.md 与实际文件一致
- [ ] 没有遗漏 frontmatter 的文件
- [ ] 没有 related 引用了不存在的 slug
- [ ] 没有空目录

### 6.2 季度整理（每季度初）

- [ ] 回顾 tags 是否过于碎片化，合并相近标签
- [ ] 检查是否有内容过时需要标注或归档
- [ ] 评估目录结构是否需要调整
- [ ] 更新 INDEX.md 统计数据

### 6.3 年度归档

- 超过 1 年且不再活跃引用的帖子类内容，移入 `posts/archive/`
- 调研报告如已过时，在 frontmatter 下方加标注：`> ⚠️ 本文档可能已过时，最后核实：YYYY-MM-DD`

---

## 7. 长期防退化约束

### 约束 1：一个文件一个主题
不要把多个不相关主题塞进同一个文件。如果一个文件超过 500 行，考虑拆分。

### 约束 2：目录层级 ≤ 3 层
`ai/prompts/image-generation/xxx.md` 是 3 层，这是上限。不要出现 `ai/llm/prompts/image/style/xxx.md`。

### 约束 3：命名一致性
同类文件的命名风格保持一致。工具调研用 `工具名.md`，提示词用 `风格或用途.md`，帖子用 `平台-作者-主题.md`。

### 约束 4：INDEX.md 是唯一入口
任何新增/修改/删除文件的操作，都必须同步更新 INDEX.md。INDEX.md 是知识库的"目录页"。

### 约束 5：不保留废弃内容
删除的文件直接 git rm，不留 `xxx-deprecated.md`。需要历史记录用 git log 查看。

### 约束 6：frontmatter 先行
正文可以随意写，但 frontmatter 必须规范。这是机器可读的结构化元数据，是索引和关联的基础。

### 约束 7：工具人（AI Agent）操作须知
当 AI Agent 被要求向知识库存入内容时，必须：
1. 阅读本规范
2. 按规范创建文件（frontmatter + 正文）
3. 更新 INDEX.md
4. git add && commit && push
5. 向用户确认已存入的位置和路径

---

## 8. 技能/资产文件

带资产的 Skill（如 cocoon-ai 的 template.html）：

```
ai/skills/cocoon-ai/
├── architecture-diagram-generator.md    # Skill 说明
└── assets/
    └── template.html                    # 配套资产
```

- 资产文件放 `assets/` 子目录
- frontmatter 中不需要列资产文件，正文内引用即可
- INDEX.md 只索引 `.md` 文件，不索引资产

---

*本规范随知识库演进，如有调整需在 git commit 中说明理由。*
