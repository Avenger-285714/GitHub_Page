# GitHub Page 项目

这是一个基于 Hexo 的个人博客项目，使用 Git Submodules 管理多个相关仓库。

## 📁 项目结构

```
GitHub_Page/
├── hexo-blog/                    # Hexo 博客源码
│   ├── source/_posts/           # 博客文章
│   ├── themes/particlex/        # 主题软链接 → hexo-theme-particlex
│   └── _config.yml              # Hexo 配置文件
├── Avenger-285714.github.io/    # GitHub Pages 部署仓库 (submodule)
└── hexo-theme-particlex/        # Hexo 主题仓库 (submodule)
```

## 🚀 快速开始

### 克隆项目

```bash
# 克隆主仓库及所有 submodules
git clone --recurse-submodules git@github.com:Avenger-285714/GitHub_Page.git

# 或者分步克隆
git clone git@github.com:Avenger-285714/GitHub_Page.git
cd GitHub_Page
git submodule update --init --recursive
```

### 安装依赖

```bash
cd hexo-blog
npm install
```

### 本地预览

```bash
cd hexo-blog
npx hexo server
# 访问 http://localhost:4000
```

### 生成静态文件

```bash
cd hexo-blog
npx hexo generate
# 生成的文件在 hexo-blog/public/ 目录
```

## 🔧 Submodules 管理

### 查看 submodules 状态

```bash
git submodule status
```

### 更新 submodules 到最新版本

```bash
# 更新所有 submodules
git submodule update --remote

# 更新特定 submodule
git submodule update --remote Avenger-285714.github.io
git submodule update --remote hexo-theme-particlex
```

### 在 submodule 中工作

```bash
# 进入 submodule 目录
cd Avenger-285714.github.io

# 正常使用 git 命令
git checkout main
git pull
git add .
git commit -m "update"
git push

# 返回主仓库，提交 submodule 引用的更新
cd ..
git add Avenger-285714.github.io
git commit -m "更新 submodule 引用"
git push
```

### 克隆已有项目后初始化 submodules

如果克隆时没有使用 `--recurse-submodules`：

```bash
git submodule init
git submodule update
```

## 📝 博客管理

### 创建新文章

```bash
cd hexo-blog
npx hexo new post "文章标题"
```

### 部署到 GitHub Pages

```bash
cd hexo-blog
npx hexo clean && npx hexo generate

# 复制生成的文件到部署仓库
cp -r public/* ../Avenger-285714.github.io/

# 提交并推送
cd ../Avenger-285714.github.io
git add .
git commit -m "更新博客内容"
git push
```

## 🎨 主题开发

主题仓库 `hexo-theme-particlex` 作为独立的 submodule 管理，通过软链接连接到 `hexo-blog/themes/particlex`。

修改主题：
```bash
cd hexo-theme-particlex
# 进行修改
git add .
git commit -m "更新主题"
git push
```

## 📚 相关链接

- [Hexo 官方文档](https://hexo.io/zh-cn/docs/)
- [Git Submodules 文档](https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E5%AD%90%E6%A8%A1%E5%9D%97)
- [GitHub Pages](https://pages.github.com/)

## 📄 License

本仓库采用混合许可模式：

- **AGPL-3.0-only**: 仓库中除 `hexo-theme-particlex` 之外的所有部分，包括主项目代码和 `Avenger-285714.github.io` 子模块，均在 **GNU Affero General Public License v3.0** 下开源。详细信息请参阅 [LICENSE](LICENSE) 文件。
- **MIT**: `hexo-theme-particlex` 子模块遵循其原始的 **MIT License**。

这意味着您在使用、修改和分发本仓库内容时，需要同时遵守这两种协议的规定。
