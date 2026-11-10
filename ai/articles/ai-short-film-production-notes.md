---
title: "AI 短片幕后：三周制作流程与工具栈（Seedance 2.5 + Nano Banana Pro + Opus 5.5）"
date: 2026-11-10
category: ai/articles
tags: [video-generation, seedance, nanobanana, opus5-5, suno, segment-anything, workflow, audio]
source: x-post
author: "@simonxxoo 团队"
related: [seedance-producer-prompt, opus-code-video-repos, video-editing-skills, palmier-pro, animation-studio-16-repos]
---

# AI 短片幕后：三周制作流程与工具栈

> 收录日期：2026-11-10
> 原文：某 AI 短片主创的幕后复盘（策划 + 制作共三周，创意制作：@simonxxoo 与作者本人）

## 一、工具栈概览

| 环节 | 工具 | 备注 |
|------|------|------|
| 视频模型 | **Seedance 2.5** | 480P 样片模式 + 定稿出正片 |
| 图像模型 | **🍌 Nano Banana Pro** | 关键帧/资产 |
| 音乐 | **Opus 5.5 + SUNO** | 主题旋律 → 分场 BGM 扩展 |
| 音效/BGM 分离 | **Segment Anything (Audio)** | Meta 出品，分离生成 BGM |
| 周期 | 策划 + 制作共 **3 周** | |

---

## 二、Seedance 2.5：480P 样片模式改变了成本结构

核心心得：

- **480P 样片模式出来后"已无对手"**，抽卡成本大幅下降。
- 流程变成：**先抽 480P 样片 → 定稿 → 再生成正片**，细节几乎完全保留（这次毛发、粒子表现很出彩）。
- 画面过锐的问题越来越少，**终稿已经不用 Topaz 了**，接近退订。

需要注意的坑：

- **样片只保留 7 天** —— 反过来也是好事，能倒逼甲方尽快确认。
- **4K 正在打折，单价居然比 1080P 还便宜** —— 出片前先看价格，别惯性选 1080P。

> 可复用结论：样片阶段用低分辨率无限试错，把"确认"变成流程里的强制节点（7 天窗口是最好的 deadline）。

---

## 三、Segment Anything (Audio)：解决 Seedance 的"顽固 BGM"

问题：Seedance 2.5 无论怎么在提示词里强调，**仍会经常自己生成 BGM**，污染后期。

解法：用 Meta 的 **Segment Anything Audio** 做音轨分离。

- 上传视频 → 输入要分离的目标（如 `background music`）→ 干净分离。
- 效果**明显好于剪映自带的分离**。

链接：

- 在线工具：<https://aidemos.meta.com/segment-anything>
- 开源地址：<https://github.com/facebookresearch/segment-anything>

部署比较麻烦，建议把「上传 → 指定分离目标 → 导出」固化成一个 **skill / workflow**，交给 Codex 每次自动跑，不用手工点。

---

## 四、声音设计：Opus 5.5 定主题，Suno 做扩展

1. 先用 **Opus 5.5** 写一条**主题旋律**。
2. 用 **Suno** 把这条主题旋律扩展成**不同场景的 BGM** → 全片音乐统一。
3. 再让 **Opus 5.5 写音效**，甚至能做到音效与前后旋律**在同一个 key 上**，听感非常统一舒适。

> 这是"音乐统一性"的廉价解法：主题旋律当锚点，Suno 负责规模化的变奏，Opus 负责细节音效与调性对齐。

---

## 五、可固化的流程（TODO）

```
策划/分镜
  → Nano Banana Pro 出关键帧 & 资产
  → Seedance 2.5 480P 样片抽卡（7 天确认窗口）
  → 定稿 → 出 4K 正片（先比价 1080P）
  → Segment Anything Audio 分离杂音轨
  → Opus 5.5 主题旋律 → Suno 扩展分场 BGM
  → Opus 5.5 写音效（同 key 对齐）
  → 剪辑合成（可不用 Topaz）
```

待办：把「Segment Anything 音频分离」封装成可复用 skill/workflow。
</content>
