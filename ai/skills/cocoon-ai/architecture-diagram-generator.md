# Architecture Diagram Generator Skill

> **原文出处**
> - 作者：Cocoon AI (hello@cocoon-ai.com)
> - 来源：GitHub
> - 链接：https://github.com/Cocoon-AI/architecture-diagram-generator
> - 版本：1.0
> - License：MIT
> - 整理时间：2026-04-15

---

## 简介

Create professional, dark-themed architecture diagrams as standalone HTML files with SVG graphics.

**触发条件：** 当用户要求系统架构图、基础设施图、云架构可视化、安全图、网络拓扑图或任何显示系统组件及其关系的技术图表时使用。

---

## 组件颜色规范

使用以下语义颜色表示不同类型的组件：

| 组件类型 | 填充色 (rgba) | 描边色 |
|----------|---------------|--------|
| **Frontend** | rgba(8, 51, 68, 0.4) | #22d3ee (cyan-400) |
| **Backend** | rgba(6, 78, 59, 0.4) | #34d399 (emerald-400) |
| **Database** | rgba(76, 29, 149, 0.4) | #a78bfa (violet-400) |
| **AWS/Cloud** | rgba(120, 53, 15, 0.3) | #fbbf24 (amber-400) |
| **Security** | rgba(136, 19, 55, 0.4) | #fb7185 (rose-400) |
| **Message Bus** | rgba(251, 146, 60, 0.3) | #fb923c (orange-400) |
| **External/Generic** | rgba(30, 41, 59, 0.5) | #94a3b8 (slate-400) |

---

## 字体规范

- **字体：** JetBrains Mono（等宽字体，技术美学）
- **组件名称：** 12px
- **子标签：** 9px
- **注释：** 8px
- **小标签：** 7px

---

## 背景样式

- **背景色：** #020617 (slate-950)
- **网格图案：** 微妙的网格背景

---

## 组件样式

### 组件框
- 圆角矩形（rx="6"）
- 1.5px 描边
- 半透明填充

### 安全组
- 虚线描边（stroke-dasharray="4,4"）
- 透明填充
- rose 颜色

### 区域边界
- 大虚线描边（stroke-dasharray="8,4"）
- amber 颜色
- rx="12"

---

## 箭头规范

### 箭头标记
```svg
<marker id="arrowhead" markerWidth="10" markerHeight="7" refX="9" refY="3.5" orient="auto">
  <polygon points="0 0, 10 3.5, 0 7" fill="#64748b" />
</marker>
```

### 箭头层级
- 在 SVG 中尽早绘制连接线（在背景网格之后），使它们渲染在组件框后面
- SVG 元素按文档顺序绘制，先绘制的箭头会出现在后面绘制的形状后面

### 透明填充遮罩
由于组件框使用半透明填充（rgba(..., 0.4)），后面的箭头会透过来。要完全遮罩箭头，在绘制半透明样式矩形之前，先在同一位置绘制一个不透明背景矩形：

```svg
<rect x="X" y="Y" width="W" height="H" rx="6" fill="#0f172a"/>
<rect x="X" y="Y" width="W" height="H" rx="6" fill="FILL_COLOR" stroke="STROKE_COLOR" stroke-width="1.5"/>
```

### 认证/安全流程
- 虚线，rose 颜色（#fb7185）

### 消息总线/事件总线
- 服务之间的小型连接器元素
- 使用 orange 颜色（#fb923c 描边，rgba(251, 146, 60, 0.3) 填充）

---

## 垂直布局规范

**关键：** 垂直堆叠组件时，确保适当的间距以避免重叠：

- **标准组件高度：** 60px（服务），80-120px（较大组件）
- **组件间最小垂直间隙：** 40px
- **内联连接器（消息总线）：** 放置在组件之间的间隙中，不要重叠

### 示例垂直布局
```
Component A: y=70, height=60 → ends at y=130
Gap: y=130 to y=170 → 40px gap, place bus at y=140 (20px tall)
Component B: y=170, height=60 → ends at y=230
```

**错误：** 在 Component B 开始于 y=170 时将消息总线放在 y=160（导致重叠）
**正确：** 在 40px 间隙（y=130 到 y=170）中将消息总线放在 y=140，居中

---

## 图例放置规范

**关键：** 将所有图例放置在所有边界框（区域边界、集群边界、安全组）之外。

- 计算所有边界结束的位置（y 位置 + 高度）
- 将图例放在最低边界下方至少 20px
- 如果需要，扩展 SVG viewBox 高度以容纳

### 示例
```
Kubernetes Cluster: y=30, height=460 → ends at y=490
Legend should start at: y=510 or below
SVG viewBox height: at least 560 to fit legend
```

**错误：** 在集群边界结束于 y=490 时将图例放在 y=470
**正确：** 将图例放在 y=510，在集群边界下方，viewBox 高度扩展

---

## 页面结构

1. **Header** - 带脉冲点指示器的标题、副标题
2. **Main SVG diagram** - 包含在圆角边框卡片中
3. **Summary cards** - 图表下方的 3 张卡片网格，包含关键详情
4. **Footer** - 最小元数据行

---

## 组件模板

### 基础组件框
```svg
<rect x="X" y="Y" width="W" height="H" rx="6" fill="FILL_COLOR" stroke="STROKE_COLOR" stroke-width="1.5"/>
<text x="CENTER_X" y="Y+20" fill="white" font-size="11" font-weight="600" text-anchor="middle">LABEL</text>
<text x="CENTER_X" y="Y+36" fill="#94a3b8" font-size="9" text-anchor="middle">sublabel</text>
```

### 摘要卡片
```html
<div class="card">
  <div class="card-header">
    <div class="card-dot COLOR"></div>
    <h3>Title</h3>
  </div>
  <ul>
    <li>• Item one</li>
    <li>• Item two</li>
  </ul>
</div>
```

---

## 自定义模板

复制并自定义 `assets/template.html` 中的模板。关键自定义点：

- 更新 `<title>` 和 header 文本
- 如果需要，修改 SVG viewBox 尺寸（默认：1000 x 680）
- 添加/删除/重新定位组件框
- 在组件之间绘制连接箭头
- 更新三个摘要卡片
- 更新 footer 元数据

---

## 输出要求

始终生成一个独立的 .html 文件，包含：

- **嵌入式 CSS**（无外部样式表，除 Google Fonts 外）
- **内联 SVG**（无外部图片）
- **无需 JavaScript**（纯 CSS 动画）

文件应能在任何现代浏览器中直接打开时正确渲染。

---

## 使用示例

适用于生成：
- 系统架构图
- 云基础设施图
- 微服务架构图
- 网络安全图
- 数据流图
- 网络拓扑图
