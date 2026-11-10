---
title: "Monid：一个余额调用 2800+ 工具的 Agent 工具市场"
date: 2026-11-11
category: ai/tools
tags: [agent, tools, mcp, cli, api, scraping, pay-per-use, openclaw]
source: web
url: "https://monid.ai/"
related: [openclaw-multi-agent-architecture, x-sukie234-api-proxy-business]
---

# Monid：一个余额调用 2800+ 工具的 Agent 工具市场

> 收录日期：2026-11-11 | 官网：<https://monid.ai/>

一句话：**把 2800+ 第三方工具（90+ 供应商）收进一个注册表，Agent 自己发现、自己调用，按次计费，一个余额走天下。**

---

## 一、解决什么问题

Agent 想用外部能力（爬虫、SEO、社媒、搜索、媒体生成、邮件…）时，通常要面对：

- 每个工具单独注册账号、单独绑卡、单独拿 API Key
- 每月一堆订阅，大部分时候用不上
- 工具藏得深，Agent 不知道自己能用什么

Monid 的做法是**把订阅制干掉**：所有工具挂在同一个 registry 上，只按实际调用付费，余额共享。

---

## 二、核心机制

两段式调用：

| 动作 | 作用 |
|------|------|
| `monid.discover()` | 用自然语言描述需求 → 返回 N 个候选工具，**按匹配度 + 价格排序** |
| `monid.run()` | 直接执行选中工具，**不需要为每个工具单独注册** |

计费：

- 单次调用低至 **$0.0013**，从同一个余额扣
- 按需付费，没有月费
- 新账号送 **$1 免费额度**；`monid balance` 查余额

---

## 三、工具覆盖（部分）

- **搜索/抓取**：Exa、TinyFish、Firecrawl、Octen、Browserbase
- **社媒/平台数据**：Reddit、TikTok、Instagram、YouTube、Amazon、Facebook、Telegram、Google Reviews
- **商业/人物数据**：Apollo、People Data Labs、Ploid、context.dev（品牌数据）、Ahrefs（SEO）
- **生成类**：Seedance 2.5（视频）、MiniMax（媒体生成）、ElevenLabs（语音）
- **其他**：AgentMail（Agent 邮箱）、Saperly（Agent 电话）、DeFiLlama

完整列表：<https://monid.ai/tools>

---

## 四、三种接入方式

同一个注册表、同一个余额，看你的 Agent 说哪种"语言"：

1. **CLI**（`@monid-ai/cli`）
2. **MCP**
3. **HTTP API**

---

## 五、接入步骤（Agent 侧）

```bash
# 1. 安装 + 初始化
npm install -g @monid-ai/cli@latest
monid setup --client <agent-name>

# 2. 存 skill（把 https://monid.ai/SKILL.md 放进 skill 目录）
#    官方推荐做法：直接把这句话丢给 Agent
#    $ set up https://monid.ai/SKILL.md

# 3. 鉴权：在 https://app.monid.ai/access/api-keys 生成 key
monid keys add -k <api-key> -l main
monid keys list

# 4. 常用命令
monid discover "..."   # 找工具
monid inspect <tool>   # 看参数 schema
monid run <tool> ...   # 执行
monid balance          # 查余额
```

脚本/Agent 调用时设 `NO_COLOR=1` 关掉颜色码。CLI 版本号和 SKILL.md frontmatter 里的 `version` **必须一致**，不一致就两边都升到最新。

---

## 六、值得注意的设计取舍

- **官方明确写了优先级**：如果用户已有专用 MCP / 自己的 API Key / 现成 CLI，就用那个，**不要走 Monid 花钱**。Monid 的定位是"补缺口"，不是替换整个工具栈。
- 所以真实用法是：**先 `discover` 看看有没有现成的，再决定要不要自己写爬虫** —— 把"告诉用户抓不到"变成最后手段。
- 开源：<https://github.com/monid-ai/monid>，工具提供方可以贡献自己的工具进托管版。

---

## 七、适合 / 不适合

**适合**

- Agent 偶尔需要某个付费数据源，不想为它开月费订阅
- 多工具编排、临时调研、一次性抓取
- 想给 Agent 一个"通用外挂"，又不想逐个接 MCP

**不适合**

- 高频、稳定调用某个工具（那时直接买订阅/自建更便宜）
- 对数据合规、请求路径有强要求的场景（多了一层中间商）
</content>
