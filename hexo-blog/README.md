# Hexo 博客项目

这是 **仿生佛能超度电子蟑螂吗** 博客的 Hexo 源码项目。

## 项目结构

```
hexo-blog/                      # Hexo 主项目（本目录）
├── _config.yml                 # Hexo 主配置文件
├── package.json                # 依赖管理
├── source/                     # 源文件目录
│   └── _posts/                 # 文章 Markdown 源文件
│       ├── 糖醋排骨.md
│       ├── 卤牛肉.md
│       └── 三杯鸡.md
├── themes/                     # 主题目录
│   └── particlex -> ../../hexo-theme-particlex  # 主题符号链接
├── public/                     # 生成的静态文件（不提交到仓库）
└── scaffolds/                  # 文章模板

../hexo-theme-particlex/        # ParticleX 主题仓库
└── （主题源码）

../Avenger-285714.github.io/    # GitHub Pages 部署仓库
└── （生成的静态网站文件）
```

## 使用说明

### 1. 安装依赖

```bash
cd /home/avenger/Projects/GitHub_Page/hexo-blog
npm install
```

### 2. 常用命令

```bash
# 创建新文章
npx hexo new "文章标题"

# 清理缓存和生成的文件
npx hexo clean

# 生成静态文件
npx hexo generate
# 或简写
npx hexo g

# 本地预览
npx hexo server
# 或简写
npx hexo s
# 访问 http://localhost:4000

# 部署到 GitHub Pages
npx hexo deploy
# 或简写
npx hexo d

# 生成并部署（一步到位）
npx hexo g -d
```

### 3. 写作流程

1. **创建新文章**：
   ```bash
   npx hexo new "文章标题"
   ```
   这会在 `source/_posts/` 下创建一个新的 Markdown 文件。

2. **编辑文章**：
   使用任何文本编辑器编辑 `source/_posts/文章标题.md`。
   
   文章格式：
   ```markdown
   ---
   title: 文章标题
   date: 2024-09-04
   categories:
     - 分类名称
   tags:
     - 标签1
     - 标签2
   ---
   
   文章内容...
   ```

3. **本地预览**：
   ```bash
   npx hexo clean && npx hexo server
   ```
   在浏览器访问 http://localhost:4000 查看效果。

4. **生成静态文件**：
   ```bash
   npx hexo generate
   ```

5. **部署到 GitHub Pages**：
   ```bash
   npx hexo deploy
   ```
   或者手动部署：
   ```bash
   # 清理旧的部署仓库内容（除了 .git）
   cd ../Avenger-285714.github.io
   find . -maxdepth 1 ! -name '.git' ! -name '.' -exec rm -rf {} +
   
   # 复制新生成的文件
   cp -r ../hexo-blog/public/* .
   
   # 提交并推送
   git add .
   git commit -m "Update blog"
   git push
   ```

### 4. 配置说明

#### Hexo 主配置 (`_config.yml`)

- **站点信息**：标题、作者等
- **URL**：`https://avenger-285714.github.io`
- **主题**：`particlex`
- **部署配置**：自动部署到 `Avenger-285714.github.io` 仓库

#### 主题配置 (`themes/particlex/_config.yml`)

- 头像、背景图片
- 导航菜单
- 侧边栏信息卡片
- 功能开关（代码高亮、图片预览等）
- 评论系统（如需要）

## 三个仓库的关系

1. **hexo-blog**（本项目）：
   - Hexo 源码项目
   - 包含 Markdown 文章源文件
   - 配置文件和主题链接
   - **不需要**推送到 GitHub（或者可以创建单独的私有仓库存储源码）

2. **hexo-theme-particlex**：
   - ParticleX 主题的 fork
   - 可以自定义修改主题
   - 已通过符号链接连接到 hexo-blog

3. **Avenger-285714.github.io**：
   - GitHub Pages 部署仓库
   - 只包含生成的静态 HTML/CSS/JS 文件
   - 网站地址：https://avenger-285714.github.io

## 当前已发布文章

- 糖醋排骨 (2024-09-04)
- 卤牛肉 (2024-09-05)
- 三杯鸡 (2024-09-05)

分类：**不想当五星大厨的程序员不是好吗喽**

## 备份建议

建议将 `hexo-blog` 目录也推送到 GitHub 作为源码备份：

```bash
cd /home/avenger/Projects/GitHub_Page/hexo-blog
git init
git add .
git commit -m "Initial commit: Hexo source files"
# 在 GitHub 创建一个新的私有仓库，然后：
git remote add origin git@github.com:Avenger-285714/blog-source.git
git push -u origin main
```

这样您就有了完整的备份，不会再丢失源文件了！

## 注意事项

- `public/` 目录的内容是自动生成的，不需要手动编辑
- 修改主题请在 `hexo-theme-particlex` 仓库中进行
- 文章源文件在 `source/_posts/` 目录
- 每次发布前建议先 `hexo clean` 清理缓存
