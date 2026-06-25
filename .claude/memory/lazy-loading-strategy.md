---
name: lazy-loading-strategy
description: 照片墙采用首屏15张+滚动懒加载策略
metadata:
  type: project
  project: yidezhong-memorial
---

照片墙使用 `IntersectionObserver` 实现渐进懒加载。

**策略：**
- 首屏立即加载前 15 张（`INITIAL_LOAD = 15`），同时添加 `.visible` 类解除 `opacity: 0`
- 其余照片通过第二个 `IntersectionObserver` 观察，进入视口 300px 范围内时加载并添加 `.visible` 类
- **注意**：照片墙元素由 `initPhotoWall()` 动态创建，全局 `initScrollAnimations()` 的 Observer 在创建前已执行完毕——因此 `.visible` 必须在照片墙自己的 `loadBatch()` 和 Observer 回调中添加，否则照片永远不可见
- 不支持 IntersectionObserver 的旧浏览器降级为全部加载
- `loadPhoto()` 根据 `window.innerWidth <= 767` 自动选择 `thumbnails-mobile/`（128px）或 `thumbnails/`（256px）
- **加载进度**（2026-06-25 新增）：底部 `.photo-progress` 元素显示 "已加载 X / 97" + 金色进度条，`updateProgress()` 在每张照片加载/失败后更新，全部完成后 1.5s 淡出
- **响应式切换**（2026-06-25 新增）：`resize` 事件监听（300ms 去抖），窗口宽度跨越 767px 断点时自动更新所有已显示 `<img>` 的 `src` 到对应缩略图目录

**Why:** 97张照片如果一次加载会严重影响首屏速度。分批加载让页面快速可交互。`.visible` 修复解决了元素创建时机与全局动画 Observer 不匹配的问题。响应式目录选择为手机端节省流量。进度条让用户知道加载状态。resize 切换确保设备旋转时缩略图质量匹配屏幕。

**How to apply:** 修改照片数量时改 `TOTAL_PHOTOS` 变量；修改首屏加载量时改 `INITIAL_LOAD`；照片命名必须保持 `photo-001.jpg` 格式；添加新照片需要同时更新 `thumbnails/`、`thumbnails-mobile/`、`full/` 三个目录。

Related: [[photo-wall-replaced-sphere]] [[photo-naming-convention]] [[deployment-and-sharing]] [[ux-enhancements-roundup]]