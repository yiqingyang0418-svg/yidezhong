---
name: photo-naming-convention
description: 照片命名必须用photo-001.jpg格式，三个尺寸版本缺一不可
metadata:
  type: project
  project: yidezhong-memorial
---

照片墙的照片遵循固定命名规则：

- **命名格式**: `photo-001.jpg`, `photo-002.jpg`, ... `photo-097.jpg`（三位数字，不足补零）
- **三个版本**（缺一不可）:
  1. `images/photos/thumbnails/` — 缩略图（照片墙显示用）
  2. `images/photos/thumbnails-mobile/` — 移动端缩略图
  3. `images/photos/full/` — 原图/大图（灯箱查看用）
- **修改数量**: 改 `TOTAL_PHOTOS` 变量（约第2020行），值必须等于实际照片数量

**Why:** JS 代码中用 `String(index + 1).padStart(3, '0')` 拼接文件名，命名不一致会导致图片加载失败。

**How to apply:** 添加新照片时，同时处理三个目录，保持编号连续。

Related: [[lazy-loading-strategy]]