---
name: project-identifier-convention
description: 所有项目文件用yidezhong-memorial标记，区别于其他个人网站项目
metadata:
  type: project
  project: yidezhong-memorial
---

本项目所有文档和记忆文件都携带 `project: yidezhong-memorial` 标识符。

**Why:** 用户计划启动其他个人网站项目（如作品集、博客等）。没有项目标识的话，AI 无法区分 CLAUDE.md、MEMORY.md 和记忆文件属于哪个项目——会把不同项目的规则混在一起。

**How to apply:**
- CLAUDE.md：顶部 YAML frontmatter 包含 `project.id`
- MEMORY.md：顶部 YAML frontmatter 包含 `project: yidezhong-memorial`
- `.claude/memory/*.md`：metadata 中包含 `project: yidezhong-memorial`
- 新建任何项目文件时，按上述模式添加标记
- 新项目使用不同 id（如 `my-portfolio`），保持模式一致

Related: [[no-build-tools]] [[photo-wall-replaced-sphere]] [[lazy-loading-strategy]] [[video-cover-design]] [[photo-naming-convention]] [[gold-theme-design]]
