# Slidev 论文汇报项目

这个项目使用 `Slidev` 编写论文汇报 PPT，入口文件是 `slides.md`。

## 本地预览

安装依赖：

```bash
npm install
```

启动本地预览：

```bash
npm run dev
```

默认访问地址：

```text
http://localhost:3030
```

## 项目结构

- `slides.md`：主幻灯片文件
- `components/`：可复用组件
- `.github/workflows/deploy.yml`：GitHub Pages 自动部署工作流

## 构建

本地构建静态页面：

```bash
npm run build
```

导出：

```bash
npm run export
```

## GitHub Pages 部署

这个项目已经添加 GitHub Pages 自动部署工作流：

- 工作流文件：`.github/workflows/deploy.yml`
- 触发方式：push 到 `main` 分支，或手动触发

### 启用步骤

1. 将当前项目推送到 GitHub 仓库。
2. 打开仓库 `Settings > Pages`。
3. 在 `Build and deployment` 中选择 `GitHub Actions`。
4. 之后每次 push 到 `main`，都会自动构建并发布。

### 访问地址

如果当前仓库名是 `report_4-18`，发布后的地址通常是：

```text
https://你的用户名.github.io/report_4-18/
```

## 与 Hexo 的关系

如果你的 Hexo 博客部署在根站点仓库：

```text
https://你的用户名.github.io/
```

那么这个 Slidev 项目不会覆盖 Hexo。

原因是：

- Hexo 根站点通常对应仓库 `prelearn-code.github.io`
- 当前 Slidev 项目是普通仓库，会发布到项目子路径：

```text
https://prelearn-code.github.io/report_4-18/
```

也就是说：

- Hexo 继续访问根地址
- Slidev 访问项目地址

二者可以同时存在，不冲突。

## 说明

GitHub Pages 工作流构建时已经自动使用仓库名作为 `base`，因此适合部署在项目子路径下，不需要额外手动改部署命令。
