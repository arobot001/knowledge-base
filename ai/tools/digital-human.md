---
title: "数字人制作工具"
date: 2026-07-31
category: ai/tools
tags: [digital-human, video, ai, voice-cloning, heygen, minimax, fish-audio, tts]
source: custom
author: 云归
related: [video-editing-skills]
---

# 数字人与语音克隆工具

> 整理日期：2026-07-31

## Fish Audio
- **地址：** <https://fish.audio/zh-CN/discovery/>
- **简介：** AI 文字转语音 & 免费语音克隆平台。支持情感控制、语速音调调节、非语言提示（笑声、咳嗽等），拥有 200 万+ 声音库，支持 8 种语言。底层模型 OpenAudio S1 逼真度接近真人，也可本地部署。
- **适用场景：** 数字人配音、有声书、播客、视频旁白等。

---

## rachel-digital-human-production
- **地址：** <https://github.com/Jingyi-Wu-Richael/rachel-digital-human-production>
- **简介：** Codex Skill，用于生产授权数字人口播视频。工作流包括：脚本/肖像/语音素材预检 → MiniMax 语音克隆配音 → HeyGen 图片驱动数字人视频 → 15 秒预览 → 用户确认后生成 1080p 正片。支持 job-state.json 全流程状态跟踪，需自备 MiniMax 和 HeyGen API Key。
- **适用场景：** 需要数字人口播视频的产品宣传、教程制作等。
- **依赖：** MiniMax API（语音克隆）、HeyGen API（图生视频）。
