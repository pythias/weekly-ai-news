# Weekly AI News - Mobile-First Design System

## 设计概览

本设计系统为 Weekly AI News 项目提供移动优先的 H5 响应式解决方案,遵循 ui-ux-pro-max 最佳实践。

---

## 设计原则

### 1. **Content-First Minimalism**
- 信息优先,减少视觉干扰
- 清晰的信息层级
- 充足的留白空间

### 2. **Modern Tech Aesthetic**
- 深色模式支持
- 渐变配色方案
- 卡片式布局

### 3. **Performance Optimized**
- 移动优先响应式
- 快速加载时间
- 流畅滚动体验

---

## 色彩系统

### Light Mode
```css
--color-primary: #3B82F6      /* 主题蓝 - 链接、按钮 */
--color-secondary: #10B981     /* 成功绿 - 徽章、强调 */
--color-accent: #F59E0B        /* 强调橙 - 特殊标记 */
--color-bg: #FFFFFF           /* 背景色 */
--color-surface: #F9FAFB      /* 卡片背景 */
--color-text: #111827         /* 主文本 */
--color-text-secondary: #6B7280  /* 次要文本 */
--color-border: #E5E7EB       /* 边框 */
```

### Dark Mode (自动切换)
```css
--color-bg: #0F172A           /* 深色背景 */
--color-surface: #1E293B      /* 卡片背景 */
--color-text: #F8FAFC         /* 主文本 */
--color-text-secondary: #94A3B8  /* 次要文本 */
--color-border: #334155       /* 边框 */
```

---

## 间距系统 (4pt Base)

```css
--space-xs: 4px      /* 最小间距 */
--space-sm: 8px      /* 小间距 */
--space-md: 16px     /* 标准间距 */
--space-lg: 24px     /* 大间距 */
--space-xl: 32px     /* 特大间距 */
--space-2xl: 48px    /* 超大间距 */
```

---

## 字体系统

### 字体族
```css
--font-sans: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif
--font-mono: "SF Mono", Monaco, Consolas, monospace
```

### 字号标尺
```css
--text-xs: 12px      /* 辅助文本 */
--text-sm: 14px      /* 次要文本 */
--text-base: 16px    /* 正文 (移动端基准) */
--text-lg: 18px      /* 强调文本 */
--text-xl: 20px      /* 小标题 */
--text-2xl: 24px     /* 标题 */
--text-3xl: 30px     /* 大标题 */
```

### 行高
```css
--leading-tight: 1.25     /* 标题 */
--leading-normal: 1.5     /* 正文 */
--leading-relaxed: 1.75   /* 长文本 */
```

---

## 组件库

### 1. Header (固定顶部导航)
- **高度**: 64px (移动) / 72px (桌面)
- **背景**: 半透明毛玻璃效果
- **功能**: Logo + 深色模式切换

### 2. Week Header (周刊标题区)
- **徽章**: 渐变配色 (蓝→绿)
- **标题**: 响应式字号 (30px-42px)
- **元信息**: 发布日期、作者

### 3. News Card (新闻卡片)
**移动端**:
- 单列布局
- 最小触摸区域: 44×44pt
- 按压反馈: scale(0.98)

**平板 (768px+)**:
- 2列网格布局

**桌面 (1024px+)**:
- 3列网格布局
- Hover 效果: 上浮 + 阴影

### 4. Section Title (板块标题)
- Emoji 图标 + 文本
- 底部边框分隔
- 固定间距系统

### 5. Footer (页脚)
- 归档链接 + RSS 订阅
- 响应式布局
- 充足的点击区域

---

## 响应式断点

```css
/* Mobile First - 默认 */
320px - 767px: 单列布局

/* Tablet */
768px - 1023px: 2列网格

/* Desktop */
1024px - 1439px: 3列网格

/* Large Desktop */
1440px+: 3列网格 (更大间距)
```

---

## 可访问性 (WCAG AA)

### ✅ 已实现
- [x] 对比度 ≥ 4.5:1 (正文)
- [x] 对比度 ≥ 3:1 (大文本)
- [x] 可见焦点状态 (2px 蓝色轮廓)
- [x] 最小触摸区域 44×44pt
- [x] Skip to main content 链接
- [x] 语义化 HTML (header, main, footer, nav, article)
- [x] ARIA labels (按钮、导航)
- [x] Reduced Motion 支持
- [x] 键盘导航友好

---

## 性能优化

### ✅ 已实现
- [x] CSS Variables 避免重复计算
- [x] Transform/Opacity 动画 (GPU 加速)
- [x] 图片懒加载 (loading="lazy")
- [x] 响应式图片 (max-width: 100%)
- [x] 字体预连接 (preconnect)
- [x] 毛玻璃效果 (backdrop-filter)
- [x] Core Web Vitals 监控脚本

---

## 使用方式

### 1. 引入样式表
```html
<link rel="stylesheet" href="/assets/css/mobile-first.css">
```

### 2. 使用布局模板
```yaml
---
layout: default  # 基础布局
---

---
layout: home     # 首页布局
---

---
layout: post     # 文章页布局
---

---
layout: archive  # 归档页布局
---
```

### 3. 深色模式自动切换
- 自动检测系统偏好 (`prefers-color-scheme`)
- 手动切换按钮 (保存到 localStorage)
- 切换动画流畅

---

## 目录结构

```
weekly-ai-news/
├── _layouts/
│   ├── default.html     # 基础布局 (header + footer + 主题切换)
│   ├── home.html        # 首页布局 (Hero + 板块介绍 + 最新文章)
│   ├── post.html        # 文章页布局 (周刊内容 + 导航)
│   └── archive.html     # 归档页布局 (年份分组 + 时间线)
├── assets/
│   └── css/
│       └── mobile-first.css  # 完整设计系统样式
├── archive.md           # 归档页
└── index.md             # 首页
```

---

## 浏览器支持

### ✅ 完全支持
- Chrome/Edge 88+
- Safari 14+
- Firefox 85+
- iOS Safari 14+
- Chrome Android 88+

### ⚠️ 部分支持 (Fallback)
- IE 11: 基础样式,无 CSS Variables
- 旧版 Safari: 无 backdrop-filter

---

## 设计灵感来源

- **GitHub Trending**: 卡片式布局
- **Hacker News**: 信息密度控制
- **Tailwind Blog**: 现代排版系统
- **Material Design 3**: 深色模式配色

---

## 维护指南

### 修改颜色
编辑 `mobile-first.css` 中的 `:root` 变量:
```css
:root {
  --color-primary: #YOUR_COLOR;
}
```

### 新增断点
```css
@media (min-width: YOUR_BREAKPOINT) {
  /* 样式 */
}
```

### 新增组件
遵循现有命名规范:
- `.news-*` - 新闻相关
- `.section-*` - 板块相关
- `.week-*` - 周刊相关

---

## FAQ

### Q: 如何调整移动端字号?
修改 `:root` 中的 `--text-base` (默认 16px)

### Q: 如何修改卡片圆角?
修改 `--radius-lg` (默认 12px)

### Q: 深色模式如何强制开启?
在 `<html>` 添加 `data-theme="dark"`

### Q: 如何增加更多断点?
在 `mobile-first.css` 末尾添加新的 `@media` 规则

---

## 更新日志

**2026-04-06**
- ✅ 初始版本发布
- ✅ 移动优先响应式设计
- ✅ 深色模式支持
- ✅ 完整可访问性实现
- ✅ 性能优化 (Core Web Vitals)

---

## 联系与反馈

如有问题或改进建议,请:
1. 在 GitHub Issues 提交问题
2. 查阅 ui-ux-pro-max 设计规范
3. 参考 WCAG 2.1 AA 标准

---

**设计师**: AI 办公助手 (基于 ui-ux-pro-max 设计系统)
**技术栈**: Jekyll + Pure CSS (无 JavaScript 依赖)
**许可**: MIT License
