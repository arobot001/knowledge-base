---
title: "小红书全套运营 Skill 合集（12 个，覆盖调研到分发全链路）"
date: 2026-11-02
category: ai/skills
tags: [skill, xiaohongshu, 小红书, 运营, content-ops, mcp, agent, social-media]
source: 网络整理
author: 云归
related: [xiaohongshu-brand-deal-playbook, xiaohongshu-recharge, video-editing-skills]
---

# 小红书全套运营 Skill 合集（12 个）

> 收藏日期：2026-11-02
> 用途：从「选题调研 → 文案/封面生产 → 排版 → 发布执行 → 多平台分发 → 数据复盘」拼出一条完整的小红书内容流水线
> 说明：Star 数为收藏时实测（2026-11-02），会随时间变化

## 全链路一览

| 环节 | Skill | 核心能力 | 适配人群 |
|------|-------|----------|----------|
| 1. 热点调研 | Agent-Reach | 跨平台内容搜索/读取 | 追热点、找选题 |
| 2. 封面配图 | baoyu-xhs-images | 文章拆成 1~10 张图文卡 | 知识博主、教程号 |
| 3. 排版发布 | xiaohongshu-mcp | 登录/搜索/发布图文视频 | 想让 AI 真操作账号 |
| 4. 多平台分发 | social-auto-upload | 视频批量上传 6 平台 | 矩阵号、多平台团队 |
| 5. 高级排版 | guizang-social-card-skill | 轮播图 + 公众号封面 | 重排版质感 |
| 6. 发布互动 | XiaohongshuSkills | 发布/评论/检索自动化 | Codex、Claude Code、OpenClaw 用户 |
| 7. 选题诊断 | xiaohongshu-ops-skill | 推荐流分析、账号诊断、爆款拆解 | 数据不稳的老号 |
| 8. 全链路创作 | Auto-Redbook-Skills | 标题→正文→配图→发布 | 新手快速跑通流程 |
| 9. 基础操作 | xiaohongshu-skills | 搜索/发布/评论 | 需要平台操作层 |
| 10. 视觉导演 | xhs-visual-director-skill | 封面结构、逐页画面方案 | 会写但不会排版 |
| 11. 封面设计 | gbro-cover-design | 3:4 封面 + 人物一致性 | 真人出镜账号 |
| 12. 竞品采集 | xhs-cli | 命令行搜索/点赞/收藏 | 竞品与爆款研究 |

---

## 1. 热点联动与跨平台调研 ｜ Agent-Reach

- **Star：** 约 107.5k
- **链接：** https://github.com/Panniantong/Agent-Reach
- **功能：** 搜索和读取小红书、X、YouTube、B站等平台内容（一个 CLI，零 API 费用）
- **适合：** 需要追踪热点、寻找选题素材、观察跨平台趋势的人
- **定位：** 运营工作流的**信息采集层**，帮助发现近期热门话题和用户讨论

## 2. 封面配图与图文卡片 ｜ baoyu-xhs-images

- **Star：** 所属仓库约 27.2k（JimLiu/baoyu-skills）
- **链接：** https://github.com/JimLiu/baoyu-skills
- **功能：** 把文章拆成 1~10 张小红书封面和内容卡片
- **适合：** 知识博主、教程类账号、AI 内容创作者
- **定位：** 支持多种视觉风格、布局、配色和水印，可直接生成系列图文

## 3. 排版发布与账号执行 ｜ xiaohongshu-mcp

- **Star：** 约 16.7k
- **链接：** https://github.com/xpzouying/xiaohongshu-mcp
- **功能：** 登录、搜索笔记、获取详情、发布图文和视频
- **适合：** 需要让 AI 实际操作小红书账号的人
- **定位：** 工作流最后的**执行环节**，可连接 Codex、Claude 等 Agent 完成上传和发布

## 4. 多平台分发 ｜ social-auto-upload

- **Star：** 约 16.0k
- **链接：** https://github.com/dreammis/social-auto-upload
- **功能：** 自动向小红书、抖音、视频号、B站、TikTok、YouTube 上传视频
- **适合：** 短视频矩阵、多账号和多平台运营团队
- **定位：** 成片后的**批量分发**，减少重复上传

## 5. 图文卡片与高级排版 ｜ guizang-social-card-skill

- **Star：** 约 7.9k
- **链接：** https://github.com/op7418/guizang-social-card-skill
- **功能：** 生成小红书轮播图、知识卡片和公众号封面对
- **适合：** 重视排版质感和视觉统一的内容创作者
- **定位：** 内置编辑风、瑞士风等视觉体系，28 种版式 + 10 套主题，单文件 HTML → PNG

## 6. 发布互动与账号操作 ｜ XiaohongshuSkills

- **Star：** 约 3.6k
- **链接：** https://github.com/white0dew/XiaohongshuSkills
- **功能：** 搜索、发布、评论和自动化互动
- **适合：** Codex、Claude Code 和 OpenClaw 用户
- **定位：** 把小红书常见操作封装成 Agent Skills，作为自动运营的执行工具

## 7. 选题策略与数据诊断 ｜ xiaohongshu-ops-skill

- **Star：** 约 2.5k
- **链接：** https://github.com/Xiangyu-CAS/xiaohongshu-ops-skill
- **功能：** 推荐流分析、账号诊断、选题生成、爆款拆解、数据复盘
- **适合：** 已有账号但选题散乱、数据不稳定的运营人员
- **定位：** 结合账号定位、历史表现和平台内容生成选题，并定位数据差异原因（可把 OpenClaw 变成运营助手）

## 8. 文案生成与全链路创作 ｜ Auto-Redbook-Skills

- **Star：** 约 2.4k
- **链接：** https://github.com/comeonzhj/Auto-Redbook-Skills
- **功能：** 生成标题、正文、封面、内容卡片并完成发布
- **适合：** 想快速跑通小红书图文流程的新手
- **定位：** 从主题输入到最终发布基本全覆盖，一体化内容生产工具

## 9. 搜索采集与发布互动 ｜ xiaohongshu-skills

- **Star：** 约 2.0k
- **链接：** https://github.com/autoclaw-cc/xiaohongshu-skills
- **功能：** 搜索笔记、获取内容、发布作品和评论互动
- **适合：** 需要一套小红书基础自动化能力的用户
- **定位：** 偏平台操作层，可与选题、文案、视觉类 Skill 组合

## 10. 封面策略与视觉导演 ｜ xhs-visual-director-skill

- **Star：** 约 1.5k
- **链接：** https://github.com/ziguishian/xhs-visual-director-skill
- **功能：** 确定视觉方向、图文页数、封面结构和逐页配图方案
- **适合：** 会写内容但不会规划封面和图文视觉的人
- **定位：** 先分析内容任务，再输出封面、逐页画面、绘图提示词和发布自检清单

## 11. 封面设计与人物一致性 ｜ gbro-cover-design

- **Star：** 约 943
- **链接：** https://github.com/pyang5166/gbro-cover-design
- **功能：** 生成 3:4 小红书封面构图与绘图提示词
- **适合：** 需要真人出镜封面、保持人物形象一致的账号
- **定位：** 三轮提问确认主题/风格/人物要求后输出封面方案（10 种构图风格）

## 12. 竞品调研与笔记采集 ｜ xhs-cli

- **Star：** 约 683
- **链接：** https://github.com/jackwener/xhs-cli
- **功能：** 搜索、阅读、点赞、收藏、评论，全在终端完成
- **适合：** 做竞品分析、爆款采集和互动研究的人
- **定位：** 选题策略前的**数据采集工具**，把热门笔记交给分析 Skill 继续处理

---

## 组合建议

- **轻量起步（单人博主）：** Agent-Reach（选题）→ Auto-Redbook-Skills（文案+配图）→ xiaohongshu-mcp（发布）
- **视觉优先（知识/教程号）：** Agent-Reach → xhs-visual-director-skill（视觉规划）→ guizang-social-card-skill（排版）→ 发布
- **数据驱动（已有账号）：** xhs-cli（采集竞品）→ xiaohongshu-ops-skill（诊断+选题）→ 创作 → 复盘
- **矩阵分发（团队）：** 创作 → social-auto-upload（6 平台批量）→ 互动维护 XiaohongshuSkills

## 注意

- 涉及自动发布/互动的 Skill 需自行承担平台风控风险，建议小号先测
- 多数 MCP/CLI 方案依赖账号登录态（Cookie），注意凭据安全
