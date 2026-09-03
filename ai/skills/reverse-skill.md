---
title: "Reverse Skill - AI 逆向/渗透/安全研究技能路由包"
date: 2026-09-03
category: ai/skills
tags: [skill, reverse-engineering, security, pentest, claude-code, ctf]
source: github
author: "zhaoxuya520"
url: "https://github.com/zhaoxuya520/reverse-skill"
related: []
---

# Reverse Skill - AI 逆向/渗透/安全研究技能路由包

- **仓库地址：** https://github.com/zhaoxuya520/reverse-skill
- **类型：** AI Agent Skill（安全方向技能路由包）
- **用途：** AI Agent 遇到 APK、二进制、前端 JS 加密、CTF 题目或渗透测试目标时，自动路由到对应方法论，检查可用工具，执行可重复工作流，而不是瞎猜命令
- **适用范围：** 授权逆向/渗透测试/安全研究（Authorized Penetration Testing / Security Research）

## 核心特性

- **AI 自动路由** — 任务 → RULES.md → MASTER-ROUTING → case-init/scope.md（先确认授权与网络画像，再动手）→ 场景 Skill → 工具/MCP/脚本 → 证据链与报告
- **44 条路由规则（R0–R45）** + 175 个回归测试用例，跨平台 CI 验证（Windows + Ubuntu）
- **45 个核心技能模块**，按场景分门别类，工具索引自动探测刷新
- **自进化经验库** — 把踩过的坑沉淀下来复用，避免重复犯错
- **客户端无关** — 核心路由与客户端适配层分离，CI 持续验证

## 覆盖场景

| 场景 | 入口 |
|------|------|
| APK / Android 分析 | skills/apk-reverse/ |
| iOS / 移动端 | skills/mobile-reverse/ |
| 二进制逆向 (exe/dll/so/elf) | skills/ida-reverse/、skills/radare2/ |
| Binary Ninja / HLIL / MLIL / MCP | skills/binary-ninja-reverse/ |
| .NET / C# | skills/dotnet-reverse/ |
| 前端 JS / 加密参数 | skills/js-reverse/ |
| DSL VM / 自定义 JS opcode VM | skills/reverse-engineering/dsl-vm-reverse/ |
| 抓包 / 请求重放 | anything-analyzer、Reqable MCP + js-reverse/ |
| 恶意软件 / YARA | skills/malware-analysis/ |
| 渗透测试 / 扫描 | skills/pentest-tools/ |
| 攻击链 / 红队编排 | skills/attack-chain/ |
| 取证复盘 / 报告交接 | skills/case-review/ |
| CTF 竞赛 | CTF-Sandbox-Orchestrator/（42 个子技能） |
| 固件 / IoT | skills/firmware-pentest/ |
| Patch diff / N-day | skills/patch-diff-exploit/ |
| Pwn / 漏洞利用开发 | skills/pwn-chain/ |
| EDR 绕过 | skills/edr-bypass-re/ |
| API / GraphQL | skills/api-security/ |
| 供应链 / SBOM | skills/supply-chain-security/ |
| LLM / AI 安全 | skills/llm-security/ |
| OLLVM 反混淆 | skills/reverse-engineering/references/ollvm-deobfuscation.md |
| 图表 / 报告生成 | skills/diagram-generator/、skills/docs-generator/ |

## 支持的 AI Agent

Claude Code、Codex、Cursor、Cline、OpenCode、Kiro 等兼容客户端

## 技术栈

- Java / JDK — jadx、apktool
- Node.js 22.12+ — JS 工具链与 MCP servers
- Python 3.x — Frida 与辅助脚本
- IDA Pro · radare2 · Ghidra · Binary Ninja（按需检测）

## 快速开始

```bash
git clone https://github.com/zhaoxuya520/reverse-skill.git
# 刷新工具索引（按平台）
bash skills/scripts/refresh-tool-index.sh    # Linux / macOS
powershell -File skills/scripts/refresh-tool-index.ps1   # Windows
```

AI Agent 直接读 `README_AI.md` 按说明接入，`skills/MASTER-ROUTING.md` 是主快速路由，`skills/routing.md` 是完整任务→技能矩阵。

## 备注

- ⚠️ 仅限授权测试与安全研究用途，仓库内置 scope/授权确认流程
- 相关教程：https://reverse.apivix.com/docs/

## 收藏日期

2026-09-03
