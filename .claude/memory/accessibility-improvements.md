---
name: accessibility-improvements
description: 无障碍改进：prefers-reduced-motion 动画降级 + 键盘焦点可见样式
metadata:
  type: project
  project: yidezhong-memorial
---

## prefers-reduced-motion 支持

尊重用户在操作系统设置中的"减少动画"偏好。

### CSS 端（约第 270 行）

```css
@media (prefers-reduced-motion: reduce) {
    *, *::before, *::after {
        animation-duration: 0.01ms !important;
        animation-iteration-count: 1 !important;
        transition-duration: 0.01ms !important;
    }
    #bg-particles, #hero-particles, #fireworks-canvas {
        display: none !important;
    }
    .scroll-hint {
        display: none;
    }
}
```

### JS 端

全局变量 `prefersReducedMotion` 在脚本顶部通过 `window.matchMedia` 检测。3 个 canvas 初始化 IIFE 均以此守卫：

```js
if (prefersReducedMotion) return;
```

被跳过的模块：
- 全页面背景粒子（`#bg-particles`）
- 开场粒子（`#hero-particles`）
- 烟花系统（`#fireworks-canvas`）

## 键盘焦点样式

导航圆点 `.nav-dot` 添加 `:focus-visible` 样式：

```css
.nav-dot:focus-visible {
    outline: none;
}
.nav-dot:focus-visible .dot-circle {
    border-color: var(--gold-light);
    box-shadow: 0 0 14px rgba(191,160,85,0.7);
    outline: 2px solid var(--gold);
    outline-offset: 3px;
}
```

保留 `:focus` 的 `outline: none`，仅 `:focus-visible`（键盘导航）时显示金色光环，鼠标点击时不显示。

## 测试方法

- Windows：设置 → 辅助功能 → 动画效果 → 关闭"在Windows中显示动画"，刷新页面
- macOS：系统设置 → 辅助功能 → 显示 → 减少动态效果，刷新页面
- 键盘导航：Tab 键在导航圆点间切换，确认焦点可见

**Why:** 运动敏感用户可能因粒子/烟花/滚动动画感到不适。键盘用户需要可见的焦点指示器才能有效导航。这两项是 Web 无障碍的基础要求。

**How to apply:** 未来添加新动画时，确保在 `prefers-reduced-motion` 媒体查询中降级，并在 JS 中检查 `prefersReducedMotion` 变量。

Related: [[background-ink-wash-particles]] [[ux-enhancements-roundup]]
