# GitHub_Page AI 工作指引

## 仓库结构
- 这是一个多子模块仓库：`hexo-blog`（Hexo 源码）、`hexo-theme-particlex`（主题仓库，MIT）、`Avenger-285714.github.io`（GitHub Pages 输出，AGPL）。首次克隆务必执行 `git clone --recurse-submodules`，后续用 `git submodule update --init --recursive` 保证同步。
- `hexo-blog/themes/particlex` 是指向 `../hexo-theme-particlex` 的符号链接；在该路径下做的任何修改都会落在主题子模块中，需要在子模块内单独提交并回到主仓库更新指针。
- `Avenger-285714.github.io` 目录保存已发布的静态站点。不要在其中手工修改 HTML；它应该始终来源于 `hexo-blog/public` 或 `hexo deploy`。

## Hexo 工作流
- 只在 `hexo-blog/` 中运行 npm：`npm install` 安装依赖；`npm run server` 启动本地预览（http://localhost:4000）；`npm run clean && npm run build` 生成干净的静态文件；`npm run deploy` 通过 `hexo-deployer-git` 推送到 `git@github.com:Avenger-285714/Avenger-285714.github.io.git` 的 `main` 分支。
- Hexo 缓存写在 `hexo-blog/db.json`。遇到内容不同步或路径异常时，先执行 `npx hexo clean` 再重新生成。
- 文章通过 `npx hexo new post "标题"` 创建，会自动生成位于 `source/_posts` 下的 Markdown 骨架并填充 front-matter。

## 内容约定
- 文章文件名遵循 `YYYY-MM-DD-标题.md`，通常按分类拆分到子目录（例如 `source/_posts/发行版开荒/2025-11-10-Ubuntu开荒.md`），但真正的分类/标签以 front-matter 为准。
- 常用 front-matter 字段：
  ```yaml
  ---
  title: Ubuntu 开荒
  date: 2025-11-10
  updated: 2025-12-02
  categories:
    - 发行版开荒
  tags:
    - Ubuntu
    - Linux
    - 系统配置
  description: |
    首页摘要，支持多行 Markdown。
  pinned: 10        # 越大越靠前
  secret: passcode  # 启用 hexo-helper-crypto 的 AES 加密
  ---
  ```
- 用 `<!-- more -->` 控制首页摘要长度；缺省会导致 ParticleX 在列表页展示全文。
- `source/about/`, `source/categories/`, `source/tags/` 定义独立页面。只在 `source/` 内编辑 Markdown，永远不要在 `public/` 中直接改动生成物。

## 主题与静态资源
- 全局样式与导航在 `hexo-theme-particlex/_config.yml` 中维护：菜单图标（Font Awesome 6）、侧边信息卡 `card.description`、背景轮播 `background`、功能开关（KaTeX、Highlight.js、图片预览、giscus 等）。
- 样式覆写放在 `hexo-theme-particlex/source/css/main.css`，组件结构位于 `hexo-theme-particlex/layout/*.ejs`，前端脚本在 `hexo-theme-particlex/source/js/`。Hexo 不做打包处理，这些文件会被原样复制到最终站点。
- 背景和静态图像位于 `hexo-theme-particlex/source/images/`，站点级图片可放 `hexo-blog/source/images/`，引用时使用站点根路径（例如 `/images/backgrounds/background1.png`）。

## 构建与发布
- 生成后的文件先落在 `hexo-blog/public/`。若不用 `hexo deploy`，需 `cp -r public/* ../Avenger-285714.github.io/`，然后在子模块内 `git add . && git commit -m "Update blog" && git push`，最后回到主仓库 `git add Avenger-285714.github.io` 记录指针。
- 更新任何子模块后，请运行 `git status --submodule` 检查指针是否已暂存，避免遗漏。
- 主仓库采用 AGPL-3.0-only，主题子模块为 MIT。新增文件时按所在目录继承对应许可证，确保引用和分发方式符合许可要求。
- **禁止破坏 `Avenger-285714.github.io` 子模块的 git 历史**：不要对该仓库执行 `git reset --hard`、`git rebase`、`git push -f` 等会改写历史的操作。如需修正错误提交，请使用 `git revert` 生成新提交来撤销变更。
- **每次构建发布后同步主仓库**：完成 `hexo deploy` 或手动推送 `Avenger-285714.github.io` 后，必须回到主仓库执行 `git add -A && git commit -m "描述信息" && git push` 将所有变更（包括子模块指针更新）同步推送到远程。
