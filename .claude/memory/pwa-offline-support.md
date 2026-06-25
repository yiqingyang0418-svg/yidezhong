---
name: pwa-offline-support
description: PWA 离线支持：manifest.json + sw.js，可添加到主屏幕、离线浏览
metadata:
  type: project
  project: yidezhong-memorial
---

## manifest.json

PWA 清单文件，定义添加到主屏幕时的名称、图标、主题色：

- `name`: "易德忠 — 永远的记忆"
- `short_name`: "易德忠纪念"
- `start_url`: "./"
- `display`: "standalone"（独立窗口，无浏览器 chrome）
- `background_color`: "#080808"（纯黑）
- `theme_color`: "#bfa055"（金色）
- `icons`: 引用 `images/og-image.jpg`（192x192 + 512x512）

## sw.js

Service Worker，提供离线缓存策略：

- **缓存名**：`yidezhong-memorial-v1`（更新内容时递增版本号）
- **安装**：缓存 `./`、`./index.html`、`./manifest.json`、`./audio/bgm.m4a`
- **激活**：清理旧版本缓存
- **fetch 策略**：
  - 导航请求（HTML）：网络优先，失败回退到缓存 `index.html`
  - 其他资源（图片/CSS/JS/字体/音频）：缓存优先，网络获取后更新缓存

## 注册方式

在 `index.html` 底部 JS 中：

```js
if ('serviceWorker' in navigator) {
    navigator.serviceWorker.register('./sw.js');
}
```

## 注意事项

- 首次访问需要联网（安装 SW），之后支持离线浏览已缓存内容
- 更新 `sw.js` 后需递增 `CACHE_NAME` 以触发缓存刷新
- 大量照片（97 张 full/thumbnails）不会被 SW 预缓存——它们在有网络时正常加载，离线时显示已加载过的（浏览器 HTTP 缓存）

**Why:** 纪念网站有长期保存的情感价值。PWA 让用户可以将网站添加到手机主屏幕，像 App 一样打开。离线支持确保在弱网或无网环境下仍能看到已访问过的内容。

**How to apply:** 修改 manifest 信息时编辑 `manifest.json`；更新内容后修改 `sw.js` 中的 `CACHE_NAME` 版本号以刷新客户端缓存。

Related: [[deployment-and-sharing]] [[ux-enhancements-roundup]]
