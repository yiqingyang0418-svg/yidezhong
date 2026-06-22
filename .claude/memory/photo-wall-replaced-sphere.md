---
name: photo-wall-replaced-sphere
description: 3D球体已改为照片墙，Three.js不再需要
metadata:
  type: project
  project: yidezhong-memorial
---

项目的第4板块原来是 Three.js 3D旋转球体展示照片，后来改成了**静态照片墙 + 懒加载**方案。

**Why:** 3D球体在移动端性能差，且照片多时加载很慢。照片墙方案更直观、性能更好、用户可以一次看到更多照片。

**How to apply:** 如果将来有人建议"加回3D球体"，需要先考虑性能问题。目前照片墙有97张照片，用 IntersectionObserver 实现懒加载（首屏加载15张，其余滚动触发）。Three.js 的 CDN 引用已经从 index.html 中移除。

Related: [[no-build-tools]] [[lazy-loading-strategy]]