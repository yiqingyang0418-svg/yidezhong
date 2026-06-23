---
name: gold-theme-design
description: 网站采用黑底+金色主题，CSS变量集中管理颜色
metadata:
  type: project
  project: yidezhong-memorial
---

网站的视觉设计采用**深邃黑色背景 + 金色点缀**的典雅风格。

**颜色系统**（在 CSS `:root` 中定义）：
- 背景：`#080808`（深黑）→ `#111111` → `#1a1a1a`
- 金色主色：`#bfa055`，浅金 `#d4c08c`，暗金 `#8b7030`
- 文字：主要 `#e8e4dc`，次要 `#8a857c`，淡色 `#5a5550`

**字体：** 中文用 `Noto Serif SC`（思源宋体），英文用 `Cormorant Garamond`

**Why:** 金色代表庄重和纪念，深色背景营造沉浸感，与纪念主题契合。

**How to apply:** 所有颜色应使用 CSS 变量（`var(--gold)` 等），不要硬编码色值。这样将来如果要调整主题色，只需改 `:root` 里的变量。

## 背景增强层

黑色背景上叠加了两层增强效果（详见 [[background-ink-wash-particles]]）：

1. **水墨纹理**：body 的 background-image 叠加9层 radial-gradient，模拟中国风水墨晕染
2. **金色粒子**：canvas #bg-particles，80颗微粒缓慢漂浮闪烁

首页 hero-section 使用半透明 rgba 径向渐变（`rgba(17,17,8,0.55)` → `rgba(8,8,8,0.25)`），末页 confession-section 无独立背景，均统一透出水墨纹理。