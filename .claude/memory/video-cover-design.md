---
name: video-cover-design
description: 视频信封封面用大字"女儿"/"儿子"文字代替视频缩略图
metadata:
  type: project
  project: yidezhong-memorial
---

两个视频（女儿的信封、儿子的信封）不使用视频自动生成的缩略图作为封面，而是在信封图标上用**大号文字"女儿"和"儿子"**作为封面。

**Why:** 视频自动缩略图在不同浏览器上表现不一致，且不够美观。大字封面与网站的金色典雅风格更统一。

**How to apply:** 如果增加或修改视频，修改 `VIDEOS` 数组（约第2142行）和 `coverTexts` 数组（约第2164行）。视频文件放在 `videos/` 文件夹。

Related: [[no-build-tools]]