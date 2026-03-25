# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Hugo static site for a personal blog deployed to GitHub Pages at `https://goudabuliu.github.io`. The site uses the PaperMod theme (via git submodule) and is configured for Chinese language (zh-CN).

## Common Development Commands

- **Local development**: `hugo server` starts a local server at `http://localhost:1313` with live reload.
- **Build site**: `hugo` generates the static site into the `public/` directory.
- **Create new post**: `hugo new posts/my-post.md` creates a new post with frontmatter template.
- **Update theme submodule**: After pulling changes, run `git submodule update --init --recursive` to sync the theme.

## Architecture

- **Configuration**: `hugo.toml` sets baseURL, language, title, and theme parameters.
- **Content**: Posts are stored in `content/posts/` as Markdown files with YAML frontmatter (title, date, draft).
- **Theme**: PaperMod theme is a git submodule under `themes/PaperMod/`. Customizations should be made by overriding templates in `layouts/` or adding CSS in `assets/`.
- **Static files**: Place images, PDFs, etc. in `static/` (accessible at site root).
- **Build output**: `public/` contains the generated HTML/CSS/JS (git‑ignored by default; manually commit for deployment).

## Content Creation

1. Use `hugo new posts/文件名.md` to create a draft.
2. Edit the Markdown file: set `draft: false` when ready to publish.
3. Frontmatter follows the archetype in `archetypes/default.md`.
4. Posts support standard Markdown and Hugo shortcodes.

## Theme Management

The PaperMod theme is pinned to a specific commit via submodule. To update:
```bash
cd themes/PaperMod
git pull origin master
cd ../..
git add themes/PaperMod
git commit -m "Update PaperMod theme"
```

Avoid modifying theme files directly; instead override them in `layouts/` or `assets/`.

## Deployment

This repository is a GitHub Pages site (`<username>.github.io`). Deployment is handled by pushing the built `public/` directory to the `master` branch (or via GitHub Actions if configured). The typical workflow:

1. Run `hugo` to rebuild `public/`.
2. Commit and push the `public/` directory (or use a CI/CD pipeline).

## 主题美化与更换

### 自定义美化
- 已添加自定义CSS文件：`assets/css/custom.css`
- 包含现代化设计：卡片阴影、动画效果、颜色优化、响应式布局
- 通过 `hugo.toml` 中的 `customCSS = ["css/custom.css"]` 加载

### 推荐的主题替代方案
如果希望更换整个主题，以下是几个美观的 Hugo 主题：

1. **Hugo-Theme-Stack** (卡片式布局，现代简洁)
   ```bash
   # 添加为子模块
   git submodule add https://github.com/CaiJimmy/hugo-theme-stack.git themes/hugo-theme-stack
   # 修改 hugo.toml: theme = "hugo-theme-stack"
   ```

2. **Hugo-Theme-Zzo** (多功能，多种布局)
   ```bash
   git submodule add https://github.com/zzossig/hugo-theme-zzo.git themes/zzo
   ```

3. **Hugo-Theme-Terminal** (极客风格，代码高亮优秀)
   ```bash
   git submodule add https://github.com/panr/hugo-theme-terminal.git themes/terminal
   ```

4. **Hello-Friend-NG** (简洁现代，支持暗色模式)
   ```bash
   git submodule add https://github.com/rhazdon/hugo-theme-hello-friend-ng.git themes/hello-friend-ng
   ```

### 主题更换步骤
1. 删除当前主题子模块（如需清理）：
   ```bash
   git submodule deinit -f themes/PaperMod
   git rm -f themes/PaperMod
   rm -rf .git/modules/themes/PaperMod
   ```

2. 添加新主题子模块（参考上方命令）

3. 更新 `hugo.toml` 中的 `theme = "新主题名称"`

4. 根据新主题文档调整配置（分类、菜单等）

### 在线资源
- [Hugo 主题库](https://themes.gohugo.io/) - 官方主题库
- [Jamstack Themes](https://jamstackthemes.dev/ssg/hugo/) - 按特性筛选
- [GitHub 搜索 "hugo-theme"](https://github.com/topics/hugo-theme) - 社区主题

## Notes

- The site is in Chinese (`languageCode = "zh-CN"`); ensure any new content respects this locale.
- The theme supports light/dark mode based on user preference (`mode = "auto"`).
- For advanced customizations, refer to the [PaperMod documentation](https://github.com/adityatelange/hugo-PaperMod).