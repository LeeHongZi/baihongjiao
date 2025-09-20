# 213宿舍网站部署指南

## 🚀 部署选项

### 1. GitHub Pages (推荐)

#### 步骤：
1. 将项目推送到GitHub仓库
2. 在仓库设置中启用GitHub Pages
3. 选择部署分支（通常是main或gh-pages）
4. 访问 `https://yourusername.github.io/dormitory-213-website`

#### 自动化部署脚本：
```bash
# 创建gh-pages分支
git checkout -b gh-pages
git push origin gh-pages

# 设置GitHub Pages
# 在GitHub仓库 Settings > Pages 中配置
```

### 2. Netlify

#### 步骤：
1. 连接GitHub仓库到Netlify
2. 设置构建命令：`npm run build`
3. 设置发布目录：`dist` 或根目录
4. 自动部署完成

#### netlify.toml 配置：
```toml
[build]
  command = "npm run build"
  publish = "dist"

[build.environment]
  NODE_VERSION = "16"

[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200
```

### 3. Vercel

#### 步骤：
1. 导入GitHub仓库到Vercel
2. 设置框架预设：Other
3. 构建命令：`npm run build`
4. 输出目录：`dist`
5. 部署完成

#### vercel.json 配置：
```json
{
  "buildCommand": "npm run build",
  "outputDirectory": "dist",
  "framework": null,
  "rewrites": [
    {
      "source": "/(.*)",
      "destination": "/index.html"
    }
  ]
}
```

### 4. 传统服务器部署

#### Apache配置 (.htaccess)：
```apache
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)$ index.html [QSA,L]

# 启用压缩
<IfModule mod_deflate.c>
    AddOutputFilterByType DEFLATE text/plain
    AddOutputFilterByType DEFLATE text/html
    AddOutputFilterByType DEFLATE text/xml
    AddOutputFilterByType DEFLATE text/css
    AddOutputFilterByType DEFLATE application/xml
    AddOutputFilterByType DEFLATE application/xhtml+xml
    AddOutputFilterByType DEFLATE application/rss+xml
    AddOutputFilterByType DEFLATE application/javascript
    AddOutputFilterByType DEFLATE application/x-javascript
</IfModule>

# 缓存设置
<IfModule mod_expires.c>
    ExpiresActive on
    ExpiresByType text/css "access plus 1 year"
    ExpiresByType application/javascript "access plus 1 year"
    ExpiresByType image/png "access plus 1 year"
    ExpiresByType image/jpg "access plus 1 year"
    ExpiresByType image/jpeg "access plus 1 year"
</IfModule>
```

#### Nginx配置：
```nginx
server {
    listen 80;
    server_name your-domain.com;
    root /var/www/dormitory-213-website;
    index index.html;

    # 启用gzip压缩
    gzip on;
    gzip_vary on;
    gzip_min_length 1024;
    gzip_types text/plain text/css text/xml text/javascript application/javascript application/xml+rss application/json;

    # 静态文件缓存
    location ~* \.(css|js|png|jpg|jpeg|gif|ico|svg)$ {
        expires 1y;
        add_header Cache-Control "public, immutable";
    }

    # SPA路由支持
    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

## 🔧 环境配置

### 开发环境
```bash
# 安装依赖
npm install

# 启动开发服务器
npm run dev
```

### 生产环境
```bash
# 构建项目
npm run build

# 启动生产服务器
npm start
```

## 📊 性能优化

### 1. 图片优化
- 使用WebP格式
- 实现懒加载
- 压缩图片大小

### 2. 代码优化
- CSS/JS压缩
- 移除未使用的代码
- 启用浏览器缓存

### 3. CDN配置
```html
<!-- 使用CDN加速 -->
<link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+SC:wght@300;400;500;700&display=swap" rel="stylesheet">
```

## 🔒 安全配置

### HTTPS设置
- 启用SSL证书
- 强制HTTPS重定向
- 设置安全头

### 内容安全策略
```html
<meta http-equiv="Content-Security-Policy" content="default-src 'self'; style-src 'self' 'unsafe-inline' https://fonts.googleapis.com https://cdnjs.cloudflare.com; font-src 'self' https://fonts.gstatic.com https://cdnjs.cloudflare.com; script-src 'self' 'unsafe-inline'; img-src 'self' data: https:;">
```

## 📈 监控和分析

### Google Analytics
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

### 性能监控
- 使用Lighthouse进行性能测试
- 监控Core Web Vitals
- 设置性能预算

## 🚨 故障排除

### 常见问题

1. **页面无法访问**
   - 检查服务器配置
   - 确认文件路径正确
   - 检查权限设置

2. **样式不生效**
   - 检查CSS文件路径
   - 确认缓存已清除
   - 检查浏览器兼容性

3. **JavaScript错误**
   - 检查控制台错误
   - 确认文件加载顺序
   - 检查浏览器支持

### 调试工具
- 浏览器开发者工具
- Lighthouse性能测试
- PageSpeed Insights

## 📞 技术支持

如有部署问题，请联系：
- 邮箱: dormitory213@example.com
- 电话: 138-0000-0000

---

**祝您部署顺利！** 🎉
