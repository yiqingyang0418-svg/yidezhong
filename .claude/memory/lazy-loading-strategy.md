---
name: lazy-loading-strategy
description: 照片墙采用首屏15张+滚动懒加载策略
metadata:
  type: project
  project: yidezhong-memorial
---

照片墙使用 `IntersectionObserver` 实现渐进懒加载。

**策略：**
- 首屏立即加载前 15 张（`INITIAL_LOAD = 15`）
- 其余照片通过 `IntersectionObserver` 观察，当照片占位元素进入视口 300px 范围内时加载
- 不支持 IntersectionObserver 的旧浏览器降级为全部加载

**Why:** 97张照片如果一次加载会严重影响首屏速度。分批加载让页面快速可交互。

**How to apply:** 修改照片数量时改 `TOTAL_PHOTOS` 变量；修改首屏加载量时改 `INITIAL_LOAD`；照片命名必须保持 `photo-001.jpg` 格式；添加新照片需要同时更新 `thumbnails/`、`thumbnails-mobile/`、`full/` 三个目录。

Related: [[photo-wall-replaced-sphere]]