---
project:
  id: yidezhong-memorial
  name: 易德忠纪念网站
  type: memorial-website
---

# 易德忠纪念网站

> 易德忠先生（1973年生）的个人纪念网站——记录一位父亲、儿子、企业家的生平与家庭记忆。

---

## 技术概览

| 项目 | 详情 |
|------|------|
| **类型** | 纯静态网页（PWA 就绪） |
| **文件** | 单文件 `index.html`，CSS/JS 全部内联；`manifest.json` + `sw.js`（PWA） |
| **字体** | Google Fonts（Noto Serif SC + Cormorant Garamond） |
| **运行方式** | **双击 `index.html` 直接打开**，不需要服务器、不需要 npm |
| **浏览器兼容** | 现代浏览器（Chrome/Edge/Firefox/Safari） |
| **项目标识** | `yidezhong-memorial` — 所有项目文件均携带此标记，用于多项目区分 |
| **部署** | GitHub Pages：`https://yiqingyang0418-svg.github.io/yidezhong/`（main 分支自动部署） |

## 文件结构

```
易德忠/
├── index.html          ← 唯一核心文件（所有代码在这里）
├── CLAUDE.md           ← 项目说明书（本文件）
├── manifest.json       ← PWA 清单（可添加到主屏幕）
├── sw.js               ← Service Worker（离线缓存）
├── .gitignore
├── audio/
│   └── bgm.m4a         ← 背景音乐
├── images/
│   ├── cover/          ← 封面照片
│   ├── timeline/       ← 时间轴照片（timeline-01~08.jpg）
│   ├── section2/       ← "关于父亲"板块照片（命名：hobby/dream/achieve/motto-01~03.jpg）
│   ├── section3/       ← "慈爱与温柔"板块照片
│   └── photos/
│       ├── thumbnails/     ← 照片墙缩略图（photo-001~097.jpg）
│       ├── thumbnails-mobile/ ← 移动端缩略图
│       └── full/           ← 灯箱大图（photo-001~097.jpg）
└── videos/
    ├── video-001.mp4   ← 女儿的信封
    └── video-002.mp4   ← 儿子的信封
```

## 页面结构（6个板块）

| 板块 | 内容 | 关键特性 |
|------|------|----------|
| **0 - 开场页** | 姓名、封面照 | 金色粒子动画 + 水墨纹理背景 |
| **1 - 身平经历** | 1973-至今时间轴 | 8个时间节点，响应式单列/双列 |
| **2 - 关于父亲** | 爱好/梦想/成就/座右铭/美食 | 5张卡片，4张含3张照片行 |
| **3 - 慈爱与温柔** | 为父/为子双栏 | 双面板，移动端堆叠 |
| **4 - 精彩瞬间** | 97张照片墙 | **懒加载**，点击查看大图（灯箱） |
| **5 - 儿女信封** | 2个视频 | 文字封面（"女儿祝福"/"儿子祝福"），弹窗播放 |
| **6 - 最后告白** | "祝老爸 父亲节快乐！" | 打字机效果 + 金色烟花 + 水墨纹理背景 |

## 核心功能

- **照片墙懒加载**：首屏加载15张，其余滚动到附近300px再加载。`loadBatch()` 和 `IntersectionObserver` 回调中均添加 `.visible` 类解除初始 `opacity: 0`
- **照片墙加载进度**：底部进度条 + 文字 "已加载 X / 97"，全部加载后自动淡出
- **缩略图保留原始比例**：`thumbnails/`（最长边256px）和 `thumbnails-mobile/`（最长边128px）均从 `full/` 原始大图按比例缩放，不裁切为正方形
- **响应式缩略图**：`loadPhoto()` 根据 `window.innerWidth <= 767` 自动选择移动端或桌面缩略图目录；`resize` 事件跨越 767px 断点时自动重载已显示图片
- **灯箱**：点击照片放大，支持左右键导航、Esc关闭
- **背景音乐**：自动播放（多次尝试），用户交互后重试；开场页 3 秒后显示 "🎵 点击右上角开启音乐" 提示，12 秒自动消失
- **视频弹窗**：点击信封卡片播放，封面显示"女儿祝福"/"儿子祝福"文字，支持 `duration` 字段显示时长
- **烟花动画**：滚动到第6板块自动触发金色烟花，离开自动停止
- **打字机效果**：第6板块"祝老爸 父亲节快乐！"逐字显示，离开后自动重置，再次进入重新播放
- **入场动画**：Intersection Observer 驱动的滚动渐显效果
- **导航圆点**：右侧固定导航，滚动高亮当前板块，`:focus-visible` 键盘焦点样式
- **返回顶部按钮**：右下角固定按钮，离开首页后显示，点击平滑滚动回顶部
- **背景水墨纹理**：body 9层径向渐变模拟中国风水墨晕染，淡金色，透明背景透出
- **背景金色粒子**：canvas #bg-particles，80颗 0.8-2.0px 金色微粒缓慢漂浮 + 闪烁光晕
- **背景层级**：canvas z-index:0 → main z-index:1 → .section-inner z-index:2，确保粒子在内容之下
- **首页/末页背景同步**：hero-section 径向渐变改为半透明 rgba，confession-section 移除不透明背景
- **Canvas 高 DPI 适配**：3 个 canvas（背景粒子、开场粒子、烟花）均乘以 `devicePixelRatio`，Retina 屏幕清晰
- **无障碍**：`prefers-reduced-motion` 媒体查询禁用所有动画 + JS 跳过 canvas 初始化；键盘焦点可见
- **PWA 离线支持**：`manifest.json` + `sw.js`，可添加到主屏幕，离线浏览
- **SEO**：JSON-LD 结构化数据（AboutPage + Person schema）
- **页面加载过渡**：body 0.8s 淡入动画，避免内容突然出现

## ⚠️ 关键约束（修改代码时必须遵守）

1. **必须支持双击 `index.html` 直接打开**——不能用任何构建工具（npm/webpack/vite 等）
2. **所有外部资源用 CDN**——Google Fonts 用 `fonts.googleapis.com`
3. **不使用 Three.js 等大型库的 npm 安装方式**——如果将来需要3D，用 CDN 的 `<script>` 标签加载
4. **照片命名规则固定**：`photo-001.jpg` ~ `photo-097.jpg`（三位数字，不足补零）
5. **添加新照片时**：需要同时准备 `thumbnails/`（缩略图，最长边256px，保留原始比例）、`thumbnails-mobile/`（移动端，最长边128px）、`full/`（大图）三个版本——**禁止裁切为正方形**
6. **视频命名**：`video-001.mp4` 格式，在 JS 中的 `VIDEOS` 数组里配置
7. **音乐文件**：`audio/bgm.m4a`，格式固定
8. **部署**：`git push origin main` → GitHub Pages 自动部署，1-2分钟后 `https://yiqingyang0418-svg.github.io/yidezhong/` 生效

## 🏷️ 项目标识约定

本项目使用 `yidezhong-memorial` 作为唯一标识符，以区分用户的其他个人网站项目。

| 文件 | 标记方式 |
|------|----------|
| `CLAUDE.md` | YAML frontmatter 中 `project.id: yidezhong-memorial` |
| `MEMORY.md` | YAML frontmatter 中 `project: yidezhong-memorial` |
| `.claude/memory/*.md` | metadata 中 `project: yidezhong-memorial` |

处理本项目时，AI 应首先检查 CLAUDE.md 的 frontmatter 确认项目身份。
新建记忆文件时，必须在 metadata 中包含 `project: yidezhong-memorial`。

## 当前状态（截至 2026-06-25）

### 已完成 ✅
- 6个板块全部完成
- 照片墙懒加载（97张照片）+ 动画修复（`.visible` 类解除 opacity）
- 照片墙加载进度条（"已加载 X / 97"）
- 缩略图保留原始比例（不再裁切为正方形），`object-fit: contain`
- 响应式缩略图自动切换（≤767px 用 128px 移动版）+ resize 事件动态切换
- 音乐按钮（播放/暂停切换，含脉冲动画）+ 开场音乐提示
- 视频封面显示"女儿"/"儿子"文字 + 支持时长显示
- 响应式适配（手机/平板/桌面）
- GitHub Pages 部署 + 微信分享链接
- **Section 2 卡片照片行**：爱好/目标与梦想/取得成就/座右铭各3张照片，flexbox横向排列；美食卡片表情图标装饰
- **中国风水墨纹理背景**：body 叠加9层径向渐变，淡金色墨韵晕染
- **金色粒子场**：80颗 0.8-2.0px 微粒缓慢漂浮 + 正弦闪烁光晕
- **首页/末页背景统一**：hero-section 半透明渐变 + confession-section 透明化
- **Canvas 高 DPI 适配**：`setupHiDPI()` 处理 3 个 canvas 的 Retina 渲染
- **`prefers-reduced-motion` 无障碍支持**：CSS 禁用动画 + JS 跳过 canvas 初始化
- **键盘焦点样式**：导航圆点 `:focus-visible` 金色光环
- **打字机可重复播放**：离开第6板块自动重置
- **返回顶部按钮**：右下角固定，非首屏区域显示
- **滚动吸附优化**：`mandatory` → `proximity`（更宽松）
- **页面加载过渡**：body fade-in 0.8s
- **SEO 结构化数据**：JSON-LD（AboutPage + Person）
- **PWA 离线支持**：`manifest.json` + `sw.js`，可添加到主屏幕

### 可优化方向
- 移动端体验进一步优化
- 照片较多时可考虑分批加载策略
- 考虑添加访客留言功能
- 视频时长的自动获取（目前需手动填写）

## 修改指南

### 修改照片数量
在 `index.html` 约第 2020 行：`const TOTAL_PHOTOS = 97;`

### 修改视频
在 `index.html` 约第 2142 行：`VIDEOS` 数组，修改 `title` 和 `filename`

### 修改背景音乐
替换 `audio/bgm.m4a` 文件即可

### 修改 Section 2 卡片照片
照片位于 `images/section2/`，命名格式 `{类型}-{序号}.jpg`（序号为 01-03）：
- `hobby-01~03.jpg` — 爱好
- `dream-01~03.jpg` — 目标与梦想
- `achieve-01~03.jpg` — 取得成就
- `motto-01~03.jpg` — 座右铭
照片通过 `.about-card-photos` 容器（flexbox）横向排列，CSS 在约第 449 行。

### 调整背景水墨纹理透明度
在 `body` 的 `background` 属性中（约第 52-70 行），修改 9 层 `radial-gradient` 的 `rgba` 透明度值。当前大面积墨韵 0.15-0.18，点缀 0.24-0.28。

### 调整背景粒子参数
在 JS 的"全页面背景粒子"模块中（约第 1684 行），可修改 `COUNT`（数量）、`size`（尺寸）、`opacity`（透明度）等参数。

### 添加新板块
在 `<main>` 内添加新的 `<section>` + 在导航圆点 `<nav>` 中添加对应的 `<a>`

### 修改 PWA 信息
- `manifest.json`：修改 `name`、`short_name`、`description` 等
- `sw.js`：修改 `CACHE_NAME`（每次更新时递增版本号以刷新缓存）

### 修改视频时长
在 `VIDEOS` 数组的 `duration` 字段填写时长字符串（如 `'0:42'`），留空则不显示

### 调整打字机文字
在 JS 的 `initConfession` 模块（约第 2075 行），修改 `fullText` 变量（当前为 `'父亲节快乐！'`）

### 调整照片墙加载进度
进度条 CSS 在 `.photo-progress` 系列类（约第 746 行）；JS 进度更新逻辑在 `updateProgress()` 函数
