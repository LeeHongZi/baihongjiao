# 213宿舍网站部署指南

## 🎯 快速部署 (推荐方案)

### 方案一：GitHub Pages (最简单)

#### 步骤 1: 初始化Git仓库
```bash
# 在项目根目录执行
git init
git add .
git commit -m "Initial commit: 213宿舍网站"
```

#### 步骤 2: 创建GitHub仓库
1. 登录 [GitHub](https://github.com)
2. 点击 "New repository"
3. 仓库名：`dormitory-213-website`
4. 设置为 Public
5. 不要勾选 "Add a README file"
6. 点击 "Create repository"

#### 步骤 3: 推送代码到GitHub
```bash
git remote add origin https://github.com/你的用户名/dormitory-213-website.git
git branch -M main
git push -u origin main
```

#### 步骤 4: 启用GitHub Pages
1. 进入仓库页面
2. 点击 "Settings" 选项卡
3. 滚动到 "Pages" 部分
4. Source 选择 "Deploy from a branch"
5. Branch 选择 "main"
6. Folder 选择 "/ (root)"
7. 点击 "Save"

#### 步骤 5: 访问网站
等待几分钟后，访问：`https://你的用户名.github.io/dormitory-213-website`

---

### 方案二：Netlify (功能丰富)

#### 步骤 1: 准备项目
确保项目已推送到GitHub仓库

#### 步骤 2: 连接Netlify
1. 访问 [Netlify](https://netlify.com)
2. 点击 "New site from Git"
3. 选择 "GitHub"
4. 授权并选择你的仓库
5. 配置构建设置：
   - Build command: `npm run build`
   - Publish directory: `dist`
6. 点击 "Deploy site"

#### 步骤 3: 自定义域名 (可选)
1. 在Netlify控制台中，进入 Site settings
2. 点击 "Domain management"
3. 添加你的自定义域名
4. 按照提示配置DNS

---

### 方案三：Vercel (性能优秀)

#### 步骤 1: 连接Vercel
1. 访问 [Vercel](https://vercel.com)
2. 点击 "Import Project"
3. 选择你的GitHub仓库
4. 框架预设选择 "Other"
5. 构建命令：`npm run build`
6. 输出目录：`dist`
7. 点击 "Deploy"

#### 步骤 2: 配置环境变量 (如需要)
在项目设置中可以添加环境变量

---

## 🛠️ 本地构建和测试

### 安装依赖
```bash
npm install
```

### 开发模式
```bash
npm run dev
```
访问 http://localhost:3000

### 生产构建
```bash
npm run build
```
构建后的文件在 `dist` 目录中

### 测试生产版本
```bash
npm start
```

---

## 🔧 高级配置

### 1. 自定义域名配置

#### GitHub Pages自定义域名
1. 在仓库根目录创建 `CNAME` 文件
2. 内容为你的域名：`example.com`
3. 在DNS设置中添加CNAME记录指向GitHub Pages

#### Netlify自定义域名
1. 在Netlify控制台添加域名
2. 按照提示配置DNS记录
3. 启用HTTPS (自动配置)

### 2. 性能优化

#### 图片优化
```bash
# 安装图片优化工具
npm install -g imagemin-cli

# 压缩图片
imagemin assets/images/*.{jpg,png} --out-dir=dist/assets/images
```

#### 代码压缩
项目已配置自动压缩，运行 `npm run build` 即可

### 3. SEO优化

在 `index.html` 中添加：
```html
<meta name="description" content="213宿舍官方网站，展示宿舍成员、活动、相册等信息">
<meta name="keywords" content="宿舍,213,大学生活,友谊,活动">
<meta property="og:title" content="213宿舍 - 温馨的家">
<meta property="og:description" content="一个充满温暖与友谊的地方">
<meta property="og:image" content="https://你的域名.com/assets/images/og-image.jpg">
```

---

## 📱 移动端优化

网站已采用响应式设计，支持：
- 手机端 (< 768px)
- 平板端 (768px - 1199px)
- 桌面端 (>= 1200px)

---

## 🔍 故障排除

### 常见问题

1. **GitHub Pages无法访问**
   - 检查仓库是否为Public
   - 确认Pages设置正确
   - 等待几分钟让CDN更新

2. **样式不生效**
   - 检查CSS文件路径
   - 清除浏览器缓存
   - 确认文件已正确上传

3. **图片不显示**
   - 检查图片路径
   - 确认图片文件已上传
   - 检查文件大小限制

### 调试工具
- 浏览器开发者工具 (F12)
- GitHub Pages状态页面
- Netlify/Vercel构建日志

---

## 🚀 自动化部署

### GitHub Actions (GitHub Pages)
创建 `.github/workflows/deploy.yml`：
```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    
    - name: Setup Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '16'
        
    - name: Install dependencies
      run: npm install
      
    - name: Build
      run: npm run build
      
    - name: Deploy
      uses: peaceiris/actions-gh-pages@v3
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./dist
```

---

## 📊 监控和分析

### Google Analytics
在 `index.html` 的 `</head>` 前添加：
```html
<!-- Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=GA_MEASUREMENT_ID"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'GA_MEASUREMENT_ID');
</script>
```

---

## 🎉 完成！

选择适合你的部署方案，按照步骤操作即可将213宿舍网站成功部署到互联网上！

**推荐顺序**：
1. 新手：GitHub Pages
2. 需要更多功能：Netlify
3. 追求性能：Vercel

如有问题，请参考项目文档或联系技术支持。
