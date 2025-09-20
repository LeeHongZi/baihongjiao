# 213宿舍网站开发指南

## 🛠️ 开发环境设置

### 系统要求
- Node.js >= 14.0.0
- npm >= 6.0.0
- Git

### 安装步骤

1. **克隆项目**
```bash
git clone https://github.com/your-username/dormitory-213-website.git
cd dormitory-213-website
```

2. **安装依赖**
```bash
npm install
```

3. **启动开发服务器**
```bash
npm run dev
```

## 📁 项目架构

### 文件结构
```
dormitory-213-website/
├── index.html              # 主页面
├── src/                    # 源代码
│   ├── styles.css         # 样式文件
│   └── script.js          # JavaScript文件
├── assets/                 # 静态资源
│   ├── images/            # 图片
│   ├── icons/             # 图标
│   └── fonts/             # 字体
├── docs/                   # 文档
│   └── deployment.md      # 部署指南
├── package.json           # 项目配置
├── .gitignore             # Git忽略文件
└── README.md              # 项目说明
```

### 代码组织

#### HTML结构
- 语义化标签
- 无障碍访问支持
- SEO优化

#### CSS架构
- 移动优先设计
- BEM命名规范
- CSS变量使用
- 响应式网格系统

#### JavaScript模块
- ES6+语法
- 模块化组织
- 事件委托
- 性能优化

## 🎨 样式指南

### 颜色系统
```css
:root {
  --primary-color: #4a90e2;
  --secondary-color: #357abd;
  --accent-color: #667eea;
  --text-color: #333;
  --text-light: #666;
  --background: #f8f9fa;
  --white: #ffffff;
}
```

### 字体系统
```css
:root {
  --font-family: 'Noto Sans SC', sans-serif;
  --font-size-xs: 0.75rem;
  --font-size-sm: 0.875rem;
  --font-size-base: 1rem;
  --font-size-lg: 1.125rem;
  --font-size-xl: 1.25rem;
  --font-size-2xl: 1.5rem;
  --font-size-3xl: 1.875rem;
  --font-size-4xl: 2.25rem;
}
```

### 间距系统
```css
:root {
  --spacing-xs: 0.25rem;
  --spacing-sm: 0.5rem;
  --spacing-md: 1rem;
  --spacing-lg: 1.5rem;
  --spacing-xl: 2rem;
  --spacing-2xl: 3rem;
  --spacing-3xl: 4rem;
}
```

## 🔧 开发工具

### 代码格式化
```bash
# 格式化代码
npm run format

# 检查代码质量
npm run lint
```

### 构建工具
```bash
# 开发构建
npm run dev

# 生产构建
npm run build

# 启动生产服务器
npm start
```

## 📱 响应式设计

### 断点设置
```css
/* 手机端 */
@media (max-width: 767px) { }

/* 平板端 */
@media (min-width: 768px) and (max-width: 1023px) { }

/* 桌面端 */
@media (min-width: 1024px) { }
```

### 网格系统
```css
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

.grid {
  display: grid;
  gap: 20px;
}

.grid-2 { grid-template-columns: repeat(2, 1fr); }
.grid-3 { grid-template-columns: repeat(3, 1fr); }
.grid-4 { grid-template-columns: repeat(4, 1fr); }
```

## ⚡ 性能优化

### 图片优化
```html
<!-- 懒加载 -->
<img src="placeholder.jpg" data-src="actual-image.jpg" class="lazy" alt="描述">

<!-- WebP支持 -->
<picture>
  <source srcset="image.webp" type="image/webp">
  <img src="image.jpg" alt="描述">
</picture>
```

### JavaScript优化
```javascript
// 防抖函数
function debounce(func, wait) {
  let timeout;
  return function executedFunction(...args) {
    const later = () => {
      clearTimeout(timeout);
      func(...args);
    };
    clearTimeout(timeout);
    timeout = setTimeout(later, wait);
  };
}

// 节流函数
function throttle(func, limit) {
  let inThrottle;
  return function() {
    const args = arguments;
    const context = this;
    if (!inThrottle) {
      func.apply(context, args);
      inThrottle = true;
      setTimeout(() => inThrottle = false, limit);
    }
  };
}
```

## 🧪 测试

### 手动测试清单
- [ ] 所有页面在移动端正常显示
- [ ] 所有链接正常工作
- [ ] 表单验证功能正常
- [ ] 动画效果流畅
- [ ] 图片加载正常
- [ ] 性能指标达标

### 自动化测试
```bash
# 运行测试
npm test

# 性能测试
npm run lighthouse
```

## 🔍 调试技巧

### 浏览器调试
1. 使用Chrome DevTools
2. 检查网络请求
3. 监控性能指标
4. 测试响应式设计

### 常见问题
1. **样式不生效**: 检查CSS选择器优先级
2. **JavaScript错误**: 查看控制台错误信息
3. **图片不显示**: 检查文件路径和格式
4. **动画卡顿**: 优化CSS动画属性

## 📝 代码规范

### HTML规范
- 使用语义化标签
- 添加alt属性
- 保持代码缩进一致
- 注释重要部分

### CSS规范
- 使用BEM命名
- 避免深层嵌套
- 使用CSS变量
- 保持选择器简洁

### JavaScript规范
- 使用const/let
- 避免全局变量
- 使用箭头函数
- 添加错误处理

## 🚀 部署流程

### 开发流程
1. 创建功能分支
2. 开发新功能
3. 测试功能
4. 提交代码
5. 创建Pull Request
6. 代码审查
7. 合并到主分支

### 发布流程
1. 更新版本号
2. 构建生产版本
3. 部署到服务器
4. 验证部署结果
5. 更新文档

## 📞 技术支持

### 开发团队
- 前端开发: dormitory213@example.com
- 技术支持: 138-0000-0000

### 资源链接
- [MDN Web Docs](https://developer.mozilla.org/)
- [CSS Tricks](https://css-tricks.com/)
- [JavaScript.info](https://javascript.info/)

---

**Happy Coding!** 🎉
