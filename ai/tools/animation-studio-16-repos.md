---
title: "100% 免费！16 个开源动作工作室仓库（AE 替代方案）"
date: 2026-11-05
category: ai/tools
tags: [animation, motion-design, vfx, video-generation, repos, open-source, remotion, three.js]
source: x-post
author: 云归
related: [opus-code-video-repos, video-editing-skills, web-motion-sites]
---

# 100% 免费！16 个开源动作工作室仓库

> 收藏日期：2026-11-05

原帖观点：一条 AI Agent（Opus 5.5）+ 这 16 个开源仓库，就能覆盖 **Motion / VFX / 3D / Sound / Export** 全流程，不用再碰 After Effects。

完整流水线：

```
Brief → Scenes → Motion → Sound → Render → Launch
```

---

## 🎬 01-03 基础动画层

### 01 Remotion — React 视频引擎
- **地址：** <https://github.com/remotion-dev/remotion>
- **简介：** 用 React 组件写视频，数据驱动、可复用、可版本管理，适合做模板化批量出片。
- **定位：** 整个流水线的「引擎」，代码即时间线。

### 02 Storyboarder — 镜头规划与分镜动画
- **地址：** <https://github.com/wonderunit/storyboarder>
- **简介：** 开源分镜工具，快速画镜头、排节奏、导出 animatic（动态分镜），在写代码前先把片子「演」一遍。

### 03 Anime.js — 动画时间线与缓动
- **地址：** <https://github.com/juliangarnier/anime>
- **简介：** 轻量 JS 动画库，时间线编排 + 缓动曲线是强项，适合做 UI/图形动效。

---

## 🧩 04-05 图形与像素

### 04 Flubber — 平滑形状变形
- **地址：** <https://github.com/veltman/flubber>
- **简介：** SVG 路径 morph 工具，两个形状之间插值过渡，做 logo 变形、图标转场的利器。

### 05 Pixelorama — 像素艺术与精灵动画
- **地址：** <https://github.com/Orama-Interactive/Pixelorama>
- **简介：** 开源像素画编辑器（Godot 做的），支持逐帧精灵动画，做复古/游戏风素材很顺手。

---

## 🌐 06-08 实时 3D 与物理

### 06 Three.js — 3D 场景、光照与摄像机
- **地址：** <https://github.com/mrdoob/three.js>
- **简介：** WebGL 事实标准，场景/材质/灯光/相机全套，纯代码渲染 3D 成片的主力。

### 07 PlayCanvas — 实时 3D 世界
- **地址：** <https://github.com/playcanvas/engine>
- **简介：** 带编辑器的 Web 3D 引擎，性能好、上手快，适合做可交互的 3D 场景。

### 08 cannon-es — 3D 物理与碰撞
- **地址：** <https://github.com/pmndrs/cannon-es>
- **简介：** 轻量 3D 物理引擎（cannon.js 的维护分支），刚体、碰撞、约束，给 3D 场景加「真实感」。

---

## ✨ 09-11 程序化几何与特效

### 09 Sverchok — Blender 内的程序化几何
- **地址：** <https://github.com/nortikin/sverchok>
- **简介：** Blender 节点式程序化建模插件，参数化生成几何体，改一个数就换一整套造型。

### 10 Effekseer — 粒子效果与风格化 VFX
- **地址：** <https://github.com/effekseer/Effekseer>
- **简介：** 跨平台粒子特效工具，火焰、爆炸、魔法阵这类风格化 VFX，游戏和动画都在用。

### 11 twigl — 实时着色器编码与 GIF 循环
- **地址：** <https://github.com/doxas/twigl>
- **简介：** 极简 WebGL 着色器试验场，写 fragment shader 实时预览，能直接导出循环 GIF，做背景/纹理很高效。

---

## 🔊 12-13 声音

### 12 Bark — 生成式语音与音效
- **地址：** <https://github.com/suno-ai/bark>
- **简介：** 文本转音频生成模型，能出人声、笑声、叹气、环境音，旁白和音效一锅端。

### 13 Pedalboard — 混响、压缩与音频效果
- **地址：** <https://github.com/spotify/pedalboard>
- **简介：** Spotify 开源的音频处理库，把 VST 式效果链写进代码：混响、压缩、EQ、限幅，批量处理很方便。

---

## 📹 14-16 录制、剪辑与交付

### 14 OBS Studio — 屏幕捕获与录制
- **地址：** <https://github.com/obsproject/obs-studio>
- **简介：** 直播/录屏标准工具，素材采集和演示录制的入口。

### 15 Shotcut — 时间线编辑与成片
- **地址：** <https://github.com/mltframework/shotcut>
- **简介：** 基于 MLT 框架的开源非线性剪辑软件，最后的时间线拼装、字幕、调色收尾。

### 16 FFmpeg — 编码、压缩与交付
- **地址：** <https://github.com/FFmpeg/FFmpeg>
- **简介：** 音视频处理的万能瑞士军刀，转码、压制、抽帧、拼接、加水印，流水线最后一公里。

---

## 按环节速查

| 环节 | 用什么 |
|------|--------|
| 剧本 / 分镜 | Storyboarder |
| 主引擎 / 模板化出片 | Remotion + Anime.js |
| 图形变形 / 像素素材 | Flubber + Pixelorama |
| 3D 场景 / 物理 | Three.js / PlayCanvas + cannon-es |
| 程序化建模 / 粒子 / 着色器 | Sverchok + Effekseer + twigl |
| 配音 / 音效 / 混音 | Bark + Pedalboard |
| 录制 / 剪辑 / 交付 | OBS + Shotcut + FFmpeg |

## 使用建议

- **纯代码路线：** Remotion 当骨架，Three.js 做画面，FFmpeg 收尾，全程可被 Agent 直接生成和迭代。
- **混合路线：** 3D/特效素材用 Blender(Sverchok) + Effekseer 出，再进 Shotcut 剪，最后 FFmpeg 压。
- **轻量动效：** Anime.js + Flubber + twigl 就够，浏览器里出片。
- 和 [Claude Opus 5.5 纯代码视频仓库合集](opus-code-video-repos.md) 配合看：那边是「案例和提示词」，这边是「工具链」。
