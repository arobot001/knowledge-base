---
title: "你不知道的 Claude Code：架构、治理与工程实践"
date: 2026-03-14
category: ai/articles
tags: [claude-code, architecture, context-engineering, skills, hooks, subagents, prompt-caching]
source: web-article
author: "Tw93 (@HiTw93)"
url: "https://x.com/HiTw93/status/2032091246588518683"
related: [openclaw-multi-agent-architecture]
---

# 你不知道的 Claude Code：架构、治理与工程实践

> **原文出处**
> - 作者：Tw93 (@HiTw93)
> - 来源：X/Twitter
> - 链接：https://x.com/HiTw93/status/2032091246588518683
> - 整理时间：2026-03-14

---

## 前言

这篇文章源于最近半年深度使用 Claude Code、两个账号每月 40 刀氪金换来的一些踩坑经验。

刚开始我也把它当 ChatBot 用，后来很快发现不对劲：上下文越来越乱、工具越来越多但效果越来越差、规则越写越长却越不遵守。折腾了一段时间，研究了 Claude Code 本身之后才意识到，这不是 Prompt 问题，而是这套系统的设计就是这样的。

---

## 目录

1. [Claude Code 六层架构](#六层架构)
2. [上下文治理](#上下文治理)
3. [Skills 设计](#skills-设计)
4. [Hooks 使用](#hooks-使用)
5. [Subagents 正确用法](#subagents-正确用法)
6. [Prompt Caching 架构影响](#prompt-caching-架构影响)
7. [CLAUDE.md 最佳实践](#claudemd-最佳实践)
8. [实用命令](#实用命令)
9. [实战案例](#实战案例)

---

## 六层架构

把 Claude Code 拆成六层来看：

```
收集上下文 → 采取行动 → 验证结果 → [完成 or 回到收集]
     ↑                    ↓
  CLAUDE.md          Hooks / 权限 / 沙箱
  Skills             Tools / MCP
  Memory
```

**核心原则**：只强化其中一层，系统就会失衡。
- CLAUDE.md 写太长 → 上下文先污染自己
- 工具堆太多 → 选择搞不清楚
- Subagents 开得到处都是 → 状态漂移
- 验证跳过 → 出了问题不知道哪里挂的

---

## 上下文治理

### 200K 上下文的真实分配

```
200K 总上下文
├── 固定开销 (~15-20K)
│   ├── 系统指令: ~2K
│   ├── 所有启用的 Skill 描述符: ~1-5K
│   ├── MCP Server 工具定义: ~10-20K  ← 最大隐形杀手
│   └── LSP 状态: ~2-5K
│
├── 半固定 (~5-10K)
│   ├── CLAUDE.md: ~2-5K
│   └── Memory: ~1-2K
│
└── 动态可用 (~160-180K)
    ├── 对话历史
    ├── 文件内容
    └── 工具调用结果
```

### 上下文加载策略

| 策略 | 用途 | 示例 |
|------|------|------|
| 始终常驻 | 项目契约/构建命令/禁止事项 | CLAUDE.md |
| 按路径加载 | 语言/目录/文件类型特定规则 | .claude/rules/ |
| 按需加载 | 工作流/领域知识 | Skills |
| 隔离加载 | 大量探索/并行研究 | Subagents |
| 不进上下文 | 确定性脚本/审计/阻断 | Hooks |

### 优化建议

- 保持 CLAUDE.md **短、硬、可执行**，优先写命令、约束、架构边界
- Anthropic 官方 CLAUDE.md 约 2.5K tokens
- 把大型参考文档拆到 Skills 的 supporting files
- 使用 `.claude/rules/` 做路径/语言规则
- 长会话主动用 `/context` 观察消耗
- 任务切换优先 `/clear`，同一任务进入新阶段用 `/compact`

### Compact Instructions

在 CLAUDE.md 中写明压缩时必须保留什么：

```markdown
## Compact Instructions

When compressing, preserve in priority order:
1. Architecture decisions (NEVER summarize)
2. Modified files and their key changes
3. Current verification status (pass/fail)
4. Open TODOs and rollback notes
5. Tool outputs (can delete, keep pass/fail only)
```

### HANDOFF.md 技巧

开新会话前，让 Claude 写一份 HANDOFF.md：

> 在 HANDOFF.md 里写清楚现在的进展。解释你试了什么、什么有效、什么没用，让下一个拿到新鲜上下文的 agent 只看这个文件就能继续完成任务。

---

## Skills 设计

### Skill 核心原则

- **描述要让模型知道"何时该用我"**，而不是"我是干什么的"
- 有完整步骤、输入、输出和停止条件
- 正文只放导航和核心约束，大资料拆到 supporting files
- 有副作用的 Skill 显式设置 `disable-model-invocation: true`

### 渐进式披露 (Progressive Disclosure)

- SKILL.md：定义任务语义、边界和执行骨架
- supporting files：提供领域细节
- 脚本：确定性收集上下文或证据

### Skill 目录结构

```
.claude/skills/
└── incident-triage/
    ├── SKILL.md
    ├── runbook.md
    ├── examples.md
    └── scripts/
        └── collect-context.sh
```

### Skill 类型示例

**类型一：检查清单型（质量门禁）**

```yaml
---
name: release-check
description: Use before cutting a release to verify build, version, and smoke test.
---

## Pre-flight (All must pass)
- [ ] `cargo build --release` passes
- [ ] `cargo clippy -- -D warnings` clean
- [ ] Version bumped in Cargo.toml
- [ ] CHANGELOG updated
- [ ] `kaku doctor` passes on clean env

## Output
Pass / Fail per item. Any Fail must be fixed before release.
```

**类型二：工作流型（标准化操作）**

```yaml
---
name: config-migration
description: Migrate config schema. Run only when explicitly requested.
disable-model-invocation: true
---

## Steps
1. Backup: `cp ~/.config/kaku/config.toml ~/.config/kaku/config.toml.bak`
2. Dry run: `kaku config migrate --dry-run`
3. Apply: remove `--dry-run` after confirming output
4. Verify: `kaku doctor` all pass

## Rollback
`cp ~/.config/kaku/config.toml.bak ~/.config/kaku/config.toml`
```

**类型三：领域专家型（封装决策框架）**

```yaml
---
name: runtime-diagnosis
description: Use when kaku crashes, hangs, or behaves unexpectedly at runtime.
---

## Evidence Collection
1. Run `kaku doctor` and capture full output
2. Last 50 lines of `~/.local/share/kaku/logs/`
3. Plugin state: `kaku --list-plugins`

## Decision Matrix
| Symptom | First Check |
|---|---|
| Crash on startup | doctor output → Lua syntax error |
| Rendering glitch | GPU backend / terminal capability |
| Config not applied | Config path + schema version |

## Output Format
Root cause / Blast radius / Fix steps / Verification command
```

### 描述符优化

```yaml
# 低效（~45 tokens）
description: |
  This skill helps you review code changes in Rust projects.
  It checks for common issues like unsafe code, error handling...
  Use this when you want to ensure code quality before merging.

# 高效（~9 tokens）
description: Use for PR reviews with focus on correctness.
```

### disable-auto-invoke 策略

| 频率 | 策略 |
|------|------|
| >1 次/会话 | 保持 auto-invoke，优化描述符 |
| <1 次/会话 | disable-auto-invoke，手动触发，描述符完全脱离上下文 |
| <1 次/月 | 移除 Skill，改为 AGENTS.md 中的文档 |

---

## Hooks 使用

### Hooks 定位

不是"自动运行的脚本"，而是把不能交给 Claude 临场发挥的事情收回确定性流程。

### 支持的 Hook 点

- **SessionStart**：注入动态上下文（Git 分支、环境变量）
- **PreToolUse/PostToolUse**：阻断修改受保护文件、Edit 后自动格式化/lint
- **Notification**：任务完成后推送通知

### Hook 配置示例

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit",
        "pattern": "*.rs",
        "hooks": [
          {
            "type": "command",
            "command": "cargo check 2>&1 | head -30",
            "statusMessage": "Running cargo check..."
          }
        ]
      }
    ],
    "Notification": [
      {
        "type": "command",
        "command": "osascript -e 'display notification \"Task completed\" with title \"Claude Code\"'"
      }
    ]
  }
}
```

### Hooks 适用场景

**适合：**
- 阻断修改受保护文件
- Edit 后自动格式化/lint/轻量校验
- SessionStart 后注入动态上下文
- 任务完成后推送通知

**不适合：**
- 需要读大量上下文的复杂语义判断
- 长时间运行的业务流程
- 需要多步推理和权衡的决策

---

## Subagents 正确用法

### 核心价值

不是"并行"，而是**隔离**。

扫代码库、跑测试、做审查这类会产生大量输出的事，交给 Subagent 做，主线程只拿摘要，不会被中间过程污染。

### 内置 Subagents

- **Explore**：只读扫库，跑 Haiku 省成本
- **Plan**：规划调研
- **General-purpose**：通用

### Subagent 配置参数

- `tools` / `disallowedTools`：限定工具权限
- `model`：探索用 Haiku/Sonnet，重要审查用 Opus
- `maxTurns`：防止跑飞
- `isolation: worktree`：隔离文件系统

### 后台运行技巧

长时间运行的 bash 命令按 `Ctrl+B` 移到后台，Claude 之后会用 BashOutput 工具查看结果。

Subagent 同理，直接告诉它「在后台跑」就行。

### 不适合用 Subagent 的情况

- 子代理权限和主线程一样宽（隔离无意义）
- 输出格式不固定，主线程拿到没法用
- 子任务之间强依赖，频繁共享中间状态

---

## Prompt Caching 架构影响

### 核心原则

> "Cache Rules Everything Around Me"

Claude Code 的整个架构都是围绕 Prompt 缓存构建的。高缓存命中率不只降低成本，也帮助创造更宽松的速率限制。

### Prompt 缓存工作原理

按**前缀匹配**工作，从请求开头到每个 `cache_control` 断点之前的内容都会被缓存。

```
Claude Code 的 Prompt 顺序：
1. System Prompt → 静态，锁定
2. Tool Definitions → 静态，锁定
3. Chat History → 动态，在后面
4. 当前用户输入 → 最后
```

### 破坏缓存的常见陷阱

- 在静态系统 Prompt 中放入带时间戳的内容
- 非确定性地打乱工具定义顺序
- 会话中途增删工具

### 动态信息处理

当前时间等动态信息放到**下一条消息**里传进去，不要动系统 Prompt：

```xml
<system-reminder>Current time: 2026-03-14 12:00</system-reminder>
```

### 模型切换成本

Prompt 缓存是**模型唯一**的。和 Opus 对话 100K token 后切换到 Haiku，需要为 Haiku 重建整个缓存，反而更贵。

**解决方案**：用 Subagent 交接，Opus 准备一条"交接消息"给另一个模型。

### defer_loading：工具延迟加载

发送轻量级 stub，只有工具名，标记 `defer_loading: true`。模型通过 ToolSearch 工具"发现"它们，完整 schema 只在选择后才加载。

---

## CLAUDE.md 最佳实践

### 定位

CLAUDE.md 是你和 Claude 之间的**协作契约**，不是团队文档，也不是知识库。里面只放那些**每次会话都得成立**的事。

### 应该包含

- 怎么 build、怎么 test、怎么跑（最核心）
- 关键目录结构与模块边界
- 代码风格和命名约束
- 那些不明显的环境坑
- 绝对不能干的事（NEVER 列表）
- 压缩时必须保留的信息（Compact Instructions）

### 不应该包含

- 大段背景介绍
- 完整 API 文档
- 空泛原则（如"写高质量代码"）
- Claude 通过读仓库即可推断的显然信息
- 大量背景资料和低频任务知识（放 Skills）

### CLAUDE.md 模板

```markdown
# Project Contract

## Build And Test

- Install: `pnpm install`
- Dev: `pnpm dev`
- Test: `pnpm test`
- Typecheck: `pnpm typecheck`
- Lint: `pnpm lint`

## Architecture Boundaries

- HTTP handlers live in `src/http/handlers/`
- Domain logic lives in `src/domain/`
- Do not put persistence logic in handlers
- Shared types live in `src/contracts/`

## Coding Conventions

- Prefer pure functions in domain layer
- Do not introduce new global state without explicit justification
- Reuse existing error types from `src/errors/`

## Safety Rails

### NEVER

- Modify `.env`, lockfiles, or CI secrets without explicit approval
- Remove feature flags without searching all call sites
- Commit without running tests

### ALWAYS

- Show diff before committing
- Update CHANGELOG for user-facing changes

## Verification

- Backend changes: `make test` + `make lint`
- API changes: update contract tests under `tests/contracts/`
- UI changes: capture before/after screenshots

## Compact Instructions

Preserve:

1. Architecture decisions (NEVER summarize)
2. Modified files and key changes
3. Current verification status (pass/fail commands)
4. Open risks, TODOs, rollback notes
```

---

## 实用命令

### 上下文管理

```bash
/context   # 查看 token 占用结构，排查 MCP 和文件读取占比
/clear     # 清空会话，同一问题被纠偏两次以上就重来
/compact   # 压缩但保留重点，配合 Compact Instructions
/memory    # 确认哪些 CLAUDE.md 真的被加载了
```

### 系统管理

```bash
/mcp       # 管理 MCP 连接，检查 token 成本，断开闲置 server
/hooks     # 管理 hooks，控制平面入口
/permissions # 查看或更新权限白名单
/sandbox   # 配置沙箱隔离，高自动化场景必备
/model     # 切换模型：Opus 用于深度推理，Sonnet 用于常规，Haiku 用于快速探索
```

### CLI 命令

```bash
claude --continue               # 恢复当前目录最近会话，隔天接着做
claude --resume                 # 打开选择器恢复历史会话
claude --continue --fork        # 从已有会话分叉，同一起点不同方案
claude --worktree              # 创建隔离 git worktree
claude -p "prompt"            # 非交互模式，接入 CI / pre-commit / 脚本
claude -p --output-format json  # 结构化输出，便于脚本消费
```

### 特殊命令

- `/simplify`：对刚改完的代码做三维检查（复用、质量、效率）
- `/rewind`：回到某个会话 checkpoint 重新总结
- `/btw`：在不打断主任务的前提下快速问侧问题
- `/insight`：让 Claude 分析当前会话，提炼值得沉淀到 CLAUDE.md 的内容
- 双击 ESC：回到上一条输入重新编辑

---

## 实战案例

### 混合语言项目配置（Rust + Lua）

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit",
        "pattern": "*.rs",
        "hooks": [{
          "type": "command",
          "command": "cargo check 2>&1 | head -30",
          "statusMessage": "Checking Rust..."
        }]
      },
      {
        "matcher": "Edit",
        "pattern": "*.lua",
        "hooks": [{
          "type": "command",
          "command": "luajit -b $FILE /dev/null 2>&1 | head -10",
          "statusMessage": "Checking Lua syntax..."
        }]
      }
    ]
  }
}
```

### 完整项目结构

```
Project/
├── CLAUDE.md
├── .claude/
│   ├── rules/
│   │   ├── core.md
│   │   ├── config.md
│   │   └── release.md
│   ├── skills/
│   │   ├── runtime-diagnosis/     # 统一收集日志、状态和依赖
│   │   ├── config-migration/      # 配置迁移回滚防污
│   │   ├── release-check/         # 发布前校验、smoke test
│   │   └── incident-triage/       # 线上故障分诊
│   ├── agents/
│   │   ├── reviewer.md
│   │   └── explorer.md
│   └── settings.json
└── docs/
    └── ai/
        ├── architecture.md
        └── release-runbook.md
```

### 使用阶段

1. **第一阶段**：学功能怎么用
2. **第二阶段**：调配置让它更顺手
3. **第三阶段**：让 agent 在约束下自己跑起来

---

## 验证标准

> 假如一个任务你说不清楚「什么叫做完」，那大概率也不适合直接扔给 Claude 自主完成。

### 验证层级

- **最低层**：命令退出码、lint、typecheck、unit test
- **中间层**：集成测试、截图对比、contract test、smoke test
- **更高层**：生产日志验证、监控指标、人工审查清单

---

## 相关资源

- **Claude Health Skill**：`npx skills add tw93/claude-health`
  - 运行 `/health` 自动检查配置状态
  - 输出优先级报告：需要立刻修 / 结构性问题 / 可以慢慢做

---

## 总结

Claude Code 的核心不是"回答"，而是一个反复循环的代理过程。六层架构需要平衡发展：

- **CLAUDE.md**：项目契约，短硬可执行
- **Skills**：按需加载的工作流
- **Hooks**：确定性约束和审计
- **Subagents**：隔离执行环境
- **Tools/MCP**：动作能力
- **验证**：确保做对、能回滚、可追踪

*这些是半年折腾下来的一些总结，如果大伙有用得更 6 的技巧，欢迎交流。*