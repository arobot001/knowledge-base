---
title: "Infinite Canvas - 本地可视化 AI 创作工作台"
date: 2026-07-28
category: ai/tools
tags: [ai-canvas, image-generation, video-generation, comfyui, workflow, local-deploy]
source: https://github.com/hero8152/Infinite-Canvas
author: 云归
---

# Infinite Canvas

> 调研日期：2026-07-28

## 简介

本地部署的可视化 AI 创作工作台，把多种 AI 生图/生视频能力统一到一个无限画布界面上调用。开源，禁止商业用途。

- **GitHub：** https://github.com/hero8152/Infinite-Canvas
- **B 站教程：** https://space.bilibili.com/78652351

## 支持的后端

- 几乎所有 OpenAI 协议的 API（含异步协议、Gemini 协议、方舟协议）
- 本地局域网 ComfyUI 工作流
- 火山引擎（包括即梦 CLI，可直接用即梦高级会员积分，支持文生图/图生图/文生视频/图生视频）
- ModelScope 免费 LLM 和图像模型
- RunningHub 工作流/AI 应用/收费模型

## 主要功能

- **画布式操作** - 在无限画布上管理和连接生成结果
- **扩展图片** - 对已有图片进行区域扩展
- **360 全景图预览截图**
- **视频帧抽取** - 从视频里抽帧作为素材
- **循环节点** - 批量自动化生成
- **Chrome 采集插件** - 从网页批量抓取图片/视频/文字到素材库
- **PS 直连插件** - Photoshop 直接调用画布上的所有功能

## 配套生态

- Chrome 扩展插件（已上线 Chrome Web Store）
- PS 直连插件
- B 站视频教程

## 定位

AI 生成能力的聚合前端。痛点：很多人手上有 ComfyUI、即梦、各种 API，但切换麻烦、没有统一画布。Infinite Canvas 把它们收拢到一个可视化界面里，加上素材管理和批量处理能力，适合需要大量生图/生视频又想本地管控工作流的人。

## 注意事项

- 已申请著作权，禁止商业用途
- 个人和公司内部可用，不能封装成商业产品
- 基于 code 二次开发须保持开源并注明来源
- README 里带了 API 代理推广链接，作者有变现意图但软件本身免费开源
