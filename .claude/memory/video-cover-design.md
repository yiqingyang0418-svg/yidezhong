---
name: video-cover-design
description: 视频信封封面用大字"女儿祝福""儿子祝福"文字标识，替代视频缩略图
metadata:
  type: project
  project: yidezhong-memorial
---

两个视频（女儿祝福、儿子祝福）不使用视频自动生成的缩略图作为封面，而是在信封图标上用**大号金色文字"女儿祝福"和"儿子祝福"**作为点击入口标识。

**Why:** 视频自动缩略图在不同浏览器上表现不一致，且不够美观。大字金色封面与网站的黑底金色典雅风格更统一。原先的"女儿""儿子"二字在深色背景上几乎不可见（仅30%不透明度），后提升至70%不透明度并增加 text-shadow 光晕。

**动态元素 Observer 注意:** 视频卡片由 JS 动态生成（`initVideoSection()`），页面初始化时的 `initScrollAnimations()` 一次性查询 `.fade-up` 元素会错过它们。因此 `initVideoSection()` 内部创建了专用的 IntersectionObserver 来观察动态卡片，否则卡片永远保持 `opacity: 0` 不可见。

**How to apply:** 如果增加或修改视频，修改 `VIDEOS` 数组（约第2145行）和 `coverTexts` 数组（约第2166行）。CSS 封面文字样式在 `.envelope-cover-text`（约第715行），当前不透明度 0.7 + text-shadow 光晕。视频文件放在 `videos/` 文件夹。

Related: [[no-build-tools]] [[lazy-loading-strategy]]
