---
name: no-build-tools
description: 项目必须支持双击index.html直接打开，不能用任何构建工具
metadata:
  type: project
  project: yidezhong-memorial
---

这个纪念网站必须支持**双击 `index.html` 直接在浏览器中打开**，不能依赖任何构建工具（npm、webpack、vite 等）。

**Why:** 使用者是非技术人员，只需要双击文件就能看到网站。项目最初尝试过用 ES module import 方式加载 Three.js，但在本地文件协议下会报 CORS 错误，所以改回 CDN 的 `<script>` 标签方式。

**How to apply:** 所有 CSS 和 JS 都内联在 index.html 中；外部资源（字体、库）通过 CDN 链接加载；不能引入需要服务器环境的依赖。

Related: [[threejs-cdn-only]] [[photo-wall-replaced-sphere]]
