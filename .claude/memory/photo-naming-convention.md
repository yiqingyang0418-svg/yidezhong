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
  1. `images/photos/thumbnails/` — 桌面缩略图（最长边256px，**保留原始宽高比，禁止裁切为正方形**）
  2. `images/photos/thumbnails-mobile/` — 移动端缩略图（最长边128px，同样保留比例）
  3. `images/photos/full/` — 原始大图（灯箱查看用，不缩放不裁切）
- **缩略图生成规则**：从 `full/` 原始大图等比缩放，`max(width, height) = 256px`（桌面）/ `128px`（移动）。CSS `object-fit: contain` 负责在正方形格子中完整显示
- **修改数量**: 改 `TOTAL_PHOTOS` 变量（约第2020行），值必须等于实际照片数量

**Why:** 之前缩略图被批量裁切为 256×256 正方形，导致横向/纵向照片丢失边缘。保留原始比例 + `object-fit: contain` 确保完整显示。JS 代码中用 `String(index + 1).padStart(3, '0')` 拼接文件名，命名不一致会导致加载失败。

**How to apply:** 添加新照片时，从 `full/` 等比缩放生成两个缩略图版本，保持编号连续。禁止使用裁切方式生成缩略图。

Related: [[lazy-loading-strategy]]