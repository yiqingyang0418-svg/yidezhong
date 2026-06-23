---
name: section2-photo-cards
description: "关于父亲"板块4张卡片各有3张照片，flexbox横向排列，移动端换行
metadata:
  type: project
  project: yidezhong-memorial
---

"关于父亲"板块（section 2）共5张卡片，其中4张包含照片行：

| 卡片 | 照片 | 文件 |
|------|------|------|
| 爱好 | 3张 | `images/section2/hobby-01~03.jpg` |
| 目标与梦想 | 3张 | `images/section2/dream-01~03.jpg` |
| 取得成就 | 3张 | `images/section2/achieve-01~03.jpg` |
| 座右铭 | 3张 | `images/section2/motto-01~03.jpg` |
| 喜欢的美食 | 无照片 | — |

**照片行实现**：使用 `<div class="about-card-photos">` 容器包裹多个 `<img class="about-card-photo">`，CSS flexbox 横向排列，8px 间距。容器内照片 `flex: 1; min-width: 0; height: 120px; object-fit: cover;`。

**移动端**（≤767px）：`flex-wrap: wrap; flex: 1 1 100px;`，照片自动换行。

**照片来源**：桌面的"易德忠个人网站信息/照片分类/关于父亲板块照片/"按子文件夹分类，复制时统一重命名为英文短名。

**CSS 位置**：`.about-card-photos` 在 index.html 约第 449 行，移动端适配约第 1185 行。

**Why:** 用户提供了按小版块分类的照片，需要全部展示。横向排列比单张照片信息更丰富，3张为一组视觉平衡。

**How to apply:** 修改照片时替换 `images/section2/` 下对应文件（保持命名 `{type}-01~03.jpg`）。如需增减照片数量，调整 `.about-card-photos` 内的 `<img>` 数量即可，CSS 自动等分宽度。
