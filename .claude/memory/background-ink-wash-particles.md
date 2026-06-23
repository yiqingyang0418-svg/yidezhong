---
name: background-ink-wash-particles
description: 网站背景增强：中国风水墨纹理（9层径向渐变）+ 金色粒子场（80颗canvas微粒）
metadata:
  type: project
  project: yidezhong-memorial
---

全页面漆黑背景上叠加了**水墨纹理**和**金色粒子**两层背景增强，使纯黑不再单调。

## 水墨纹理

实现在 `body` 的 `background` 属性（多层 background-image 叠加），包含9层径向渐变：

| 层级 | 形状 | 尺寸 | 透明度 | 效果 |
|------|------|------|--------|------|
| 大面积山岚（3层）| ellipse | 1100-1400px | 0.15-0.18 | 大面积淡金墨韵 |
| 中层晕染（3层）| ellipse | 500-600px | 0.10-0.12 | 中层过渡 |
| 浓墨点缀（3层）| circle | 140-180px | 0.24-0.28 | 小面积深色墨迹 |

最底层为 `var(--bg-deep)` (#080808) 纯黑。

**CSS 位置**：`body` 样式块，index.html 约第 52-70 行。

**透明度调整历史**：初版 0.01-0.025（太淡不可见）→ 0.04-0.12（仍不可见）→ 当前 0.10-0.28。如需微调，修改 `rgba` 第4个参数。

## 金色粒子场

使用 `<canvas id="bg-particles">` 全页面固定定位，80颗金色微粒：

| 参数 | 值 |
|------|-----|
| 数量 | 80 颗 |
| 尺寸 | 0.8-2.0px |
| 基础透明度 | 0.2-0.5 |
| 闪烁幅度 | ±0.28（正弦波） |
| 峰值透明度 | 0.85 |
| 移动速度 | 竖直 0.08-0.30 px/frame，水平 ±0.075 |
| 光晕 | 尺寸>0.7px 的粒子带 2.5 倍弱光晕 |

**JS 位置**：index.html 约第 1684-1756 行，IIFE 自执行。

**性能优化**：页面切后台（`visibilitychange`）时暂停 `requestAnimationFrame`。

## 层级结构

```
html background (#080808)          ← 最底层
body background (水墨9层 + #080808)
#bg-particles canvas (z-index: 0)  ← 粒子层
main (z-index: 1)                  ← 内容层
  └── .section-inner (z-index: 2)  ← 卡片等
```

**Why:** 初版使用 `body::before` + `z-index: -1` 实现水墨纹理，经两次迭代后改为 body 直接 background-image + canvas z-index:0/main z-index:1 方案，避免负 z-index 在部分浏览器的渲染问题。

**How to apply:** 修改透明度在 body 的 background 属性；修改粒子在 JS 的 BgParticle 类和 COUNT 常量。要撤回背景效果，运行 `git revert` 撤销相关 commit。
