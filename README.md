# 知识库

个人知识管理系统，收集整理 AI、工具、提示词、文章和灵感。

## 目录结构

```
knowledge-base/
├── README.md                          # 本文件
├── INDEX.md                           # 知识索引（全量条目地图）
├── MAINTENANCE.md                     # 维护规范与长期迭代约束
├── ai/                                # AI 相关知识
│   ├── agents/                        # Agent 设计与实践
│   ├── articles/                      # 文章/学习笔记
│   ├── prompts/                       # 提示词工程
│   │   ├── image-generation/          # 图像生成提示词
│   │   ├── video-generation/          # 视频生成提示词
│   │   └── prompt-engineering/        # 通用提示词工程
│   ├── skills/                        # AI Skills/插件配置
│   └── tools/                         # 工具调研与推荐
├── inspirations/                      # 灵感记录
└── posts/                             # 社媒帖子收藏
```

## 组织原则

- **按类型分目录**：文件按内容类型（文章/提示词/工具调研/Skill）归类
- **主题走标签**：具体主题通过 frontmatter 的 `tags` 字段标注，不靠目录层级
- **关联走引用**：相关条目通过 frontmatter 的 `related` 字段互联
- **一个文件一个主题**：避免大杂烩，需要综合时建索引页

## 文件规范

每个 `.md` 文件必须包含 YAML frontmatter：

```yaml
---
title: "文件标题"
date: 2026-07-26              # 创建或最后更新日期
category: ai/tools             # 对应目录路径
tags: [tag1, tag2]            # 主题标签
source: web-article            # 来源类型
author: "作者"                 # 如有
url: "https://..."             # 如有原文链接
related: [other-file-slug]    # 关联条目（文件名不含扩展名）
---
```

### source 类型

| 值 | 含义 |
|---|---|
| `custom` | 自创内容 |
| `web-article` | 网络文章 |
| `web-research` | 调研报告 |
| `github` | GitHub 项目 |
| `x-post` | X/Twitter 帖子 |
| `web` | 其他网页 |

## 使用方式

1. **新增内容** → 参考 [MAINTENANCE.md](./MAINTENANCE.md)
2. **查找内容** → 查看 [INDEX.md](./INDEX.md)
3. **提交推送** → `git add . && git commit -m "描述" && git push`
