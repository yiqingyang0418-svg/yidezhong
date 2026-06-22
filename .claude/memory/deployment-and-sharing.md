---
name: deployment-and-sharing
description: 网站部署在 GitHub Pages，微信分享链接指向 github.io
metadata:
  type: project
  project: yidezhong-memorial
---

## 部署地址

微信分享链接：`https://yiqingyang0418-svg.github.io/yidezhong/`

GitHub 仓库：`https://github.com/yiqingyang0418-svg/yidezhong.git`

## 部署机制

- GitHub Pages 从 `main` 分支根目录自动部署
- **没有** CI/CD pipeline、没有 gh-pages 分支、没有构建步骤
- 只需 `git push origin main`，1-2 分钟后自动生效
- 本地修改不会自动同步到线上——必须 commit + push

## 用户触发词

用户说以下任何一句话，都表示要把本地修改推送到 GitHub Pages：

- "同步到手机链接" / "更新微信链接" / "更新分享链接"
- "推送到线上" / "部署" / "发布"
- "让手机端也能看到" / "微信打开还是旧的"
- "push 到 GitHub" / "更新 github.io"

**How to apply:**
1. `git add` 所有修改的文件
2. `git commit -m "<描述>"` 
3. `git push origin main`
4. 告知用户 1-2 分钟后 `https://yiqingyang0418-svg.github.io/yidezhong/` 生效

Related: [[project-identifier-convention]]
