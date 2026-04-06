# Weekly AI News - 优化计划

## 📊 项目现状分析

**已完成**:
- ✅ 移动优先响应式设计系统
- ✅ 深色模式支持
- ✅ 自定义 Jekyll 布局 (4 个)
- ✅ WCAG AA 可访问性
- ✅ 性能优化 (GPU 加速动画)

**待优化项**:
- ⚠️ minima 主题冲突
- ⚠️ 缺少真实内容数据
- ⚠️ 配置信息占位符
- ⚠️ 缺少实用功能

---

## 🔴 高优先级优化 (立即实施)

### 1. ✅ 移除 minima 主题避免样式冲突

**问题**: `_config.yml` 中 `theme: minima` 会与自定义样式产生冲突

**解决**: 已注释掉 minima 主题配置

**影响**: 确保使用纯自定义设计系统,无样式覆盖问题

---

### 2. 添加代码语法高亮样式

**问题**: 文章中有代码块,但缺少 Rouge 高亮主题

**解决方案**:

创建 `assets/css/syntax-highlighting.css`:

```css
/* Rouge Syntax Highlighting - Dark/Light Mode */
.highlight {
  background-color: var(--color-surface);
  border: 1px solid var(--color-border);
  border-radius: var(--radius-md);
  padding: var(--space-lg);
  overflow-x: auto;
  margin: var(--space-lg) 0;
}

/* Light Mode */
.highlight .c { color: #6a737d; } /* Comment */
.highlight .k { color: #d73a49; } /* Keyword */
.highlight .s { color: #032f62; } /* String */
.highlight .nf { color: #6f42c1; } /* Function */

/* Dark Mode */
@media (prefers-color-scheme: dark) {
  .highlight .c { color: #8b949e; }
  .highlight .k { color: #ff7b72; }
  .highlight .s { color: #a5d6ff; }
  .highlight .nf { color: #d2a8ff; }
}
```

**优先级**: 高 (影响文章阅读体验)

---

### 3. 添加社交分享按钮

**问题**: 文章页缺少分享功能,不利于传播

**解决方案**:

在 `_layouts/post.html` 中添加分享组件:

```html
<!-- Social Share Buttons -->
<div class="share-buttons" style="margin-top: var(--space-xl); padding: var(--space-lg); background: var(--color-surface); border-radius: var(--radius-lg);">
  <h4 style="margin-bottom: var(--space-md);">📢 Share This Week's News</h4>
  <div style="display: flex; gap: var(--space-md); flex-wrap: wrap;">
    <a href="https://twitter.com/intent/tweet?url={{ page.url | absolute_url }}&text={{ page.title }}"
       target="_blank" class="archive-link">
      Twitter
    </a>
    <a href="https://www.linkedin.com/sharing/share-offsite/?url={{ page.url | absolute_url }}"
       target="_blank" class="archive-link">
      LinkedIn
    </a>
    <a href="mailto:?subject={{ page.title }}&body={{ page.url | absolute_url }}"
       class="archive-link">
      Email
    </a>
  </div>
</div>
```

**优先级**: 高 (增强用户参与度)

---

### 4. 添加 RSS 订阅浮动按钮

**问题**: RSS 订阅入口不够明显

**解决方案**:

在 `mobile-first.css` 中添加浮动按钮:

```css
/* Floating RSS Button */
.rss-float {
  position: fixed;
  bottom: var(--space-xl);
  right: var(--space-xl);
  width: 56px;
  height: 56px;
  background: linear-gradient(135deg, var(--color-primary), var(--color-secondary));
  border-radius: 50%;
  box-shadow: var(--shadow-lg);
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-size: 24px;
  z-index: 999;
  transition: transform 150ms ease;
}

.rss-float:hover {
  transform: scale(1.1);
}

@media (max-width: 768px) {
  .rss-float {
    bottom: var(--space-lg);
    right: var(--space-lg);
  }
}
```

**优先级**: 中 (提升订阅转化率)

---

## 🟡 中优先级优化 (短期实施)

### 5. 实现文章内目录导航

**问题**: 长文章缺少快速导航

**解决方案**:

使用 JavaScript 自动生成目录:

```javascript
// Table of Contents Generator
document.addEventListener('DOMContentLoaded', function() {
  const content = document.querySelector('.post-content');
  const headings = content.querySelectorAll('h2, h3');

  if (headings.length > 3) {
    const toc = document.createElement('nav');
    toc.className = 'toc';
    toc.innerHTML = '<h4>📑 目录</h4><ul></ul>';

    headings.forEach((heading, index) => {
      const id = `heading-${index}`;
      heading.id = id;

      const li = document.createElement('li');
      li.innerHTML = `<a href="#${id}">${heading.textContent}</a>`;
      toc.querySelector('ul').appendChild(li);
    });

    content.insertBefore(toc, content.firstChild);
  }
});
```

**优先级**: 中 (改善长文章体验)

---

### 6. 添加阅读进度条

**问题**: 用户无法感知阅读进度

**解决方案**:

```css
/* Reading Progress Bar */
.reading-progress {
  position: fixed;
  top: 64px;
  left: 0;
  height: 3px;
  background: linear-gradient(90deg, var(--color-primary), var(--color-secondary));
  transition: width 150ms ease;
  z-index: 1001;
}
```

```javascript
// Update progress on scroll
window.addEventListener('scroll', () => {
  const scrolled = window.scrollY;
  const height = document.documentElement.scrollHeight - window.innerHeight;
  const progress = (scrolled / height) * 100;
  document.querySelector('.reading-progress').style.width = `${progress}%`;
});
```

**优先级**: 中 (视觉反馈优化)

---

### 7. 搜索功能 (客户端 Lunr.js)

**问题**: 缺少内容搜索功能

**解决方案**: 集成 Lunr.js 实现静态站点全文搜索

**实现成本**: 需要生成搜索索引 JSON

**优先级**: 中 (内容量增长后必需)

---

### 8. 标签云 & 分类筛选

**问题**: 无法按主题浏览内容

**解决方案**: 创建标签页面和分类筛选器

**优先级**: 中 (内容组织优化)

---

## 🟢 低优先级优化 (长期规划)

### 9. PWA 支持

- Service Worker 离线缓存
- Web App Manifest
- 添加到主屏幕提示

**优先级**: 低 (锦上添花)

---

### 10. 评论系统

**选项**:
- Giscus (GitHub Discussions)
- Utterances (GitHub Issues)
- Disqus (第三方)

**优先级**: 低 (社区规模小时不必要)

---

### 11. Newsletter 邮件订阅

- 集成 Mailchimp / ConvertKit
- 自动发送周报邮件
- 订阅表单

**优先级**: 低 (需要邮件服务成本)

---

### 12. 国际化 (i18n)

- 中文版本支持
- 多语言切换

**优先级**: 低 (目标受众主要为英文用户)

---

## 🔧 技术债务清理

### 13. 清理占位符配置

**需修改**:
- `_config.yml`: email, twitter_username, github_username
- `_config.yml`: github_repo 更新为实际仓库地址

**优先级**: 高 (基础信息完善)

---

### 14. 添加 robots.txt

```txt
User-agent: *
Allow: /

Sitemap: https://YOUR_DOMAIN/sitemap.xml
```

**优先级**: 中 (SEO 优化)

---

### 15. 添加 Open Graph 图片

创建默认分享图片 (1200×630px):

```yaml
# _config.yml
defaults:
  - scope:
      path: ""
      type: "posts"
    values:
      image: /assets/images/og-default.png
```

**优先级**: 中 (社交分享优化)

---

## 📈 性能优化建议

### 16. 图片懒加载

在 `_layouts/post.html` 中添加:

```html
<img src="..." loading="lazy" alt="...">
```

**优先级**: 高 (Core Web Vitals)

---

### 17. 字体子集化

使用 `&text=` 参数只加载需要的字符:

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
```

**优先级**: 中 (减少字体加载时间)

---

### 18. 关键 CSS 内联

将首屏 CSS 提取到 `<head>` 中:

```html
<style>
  /* Critical CSS */
  body { font-family: sans-serif; }
  .header-mobile { height: 64px; }
</style>
<link rel="stylesheet" href="/assets/css/mobile-first.css" media="print" onload="this.media='all'">
```

**优先级**: 低 (复杂度高,收益中等)

---

## 🎯 内容质量优化

### 19. 添加文章模板

创建 `_drafts/template.md`:

```markdown
---
layout: post
title: "Weekly AI News - Week XX, 2026"
date: 2026-XX-XX
categories: [weekly, ai-news]
tags: [artificial-intelligence, machine-learning]
week: XX
year: 2026
---

## 🔥 Trending This Week
[内容...]

## 🚀 New Releases
[内容...]

## 📚 Research Highlights
[内容...]
```

**优先级**: 高 (提升内容质量一致性)

---

### 20. 自动化工作流增强

优化 `.github/workflows/weekly-publish.yml`:

- 自动生成周刊框架
- 自动收集 GitHub Trending
- 自动发送通知

**优先级**: 中 (减少手动工作量)

---

## 🚀 快速实施计划

**本周 (Week 1)**:
1. ✅ 移除 minima 主题
2. 添加代码语法高亮
3. 添加社交分享按钮
4. 清理占位符配置

**下周 (Week 2)**:
5. 添加 RSS 浮动按钮
6. 实现阅读进度条
7. 添加文章内目录
8. 优化 Open Graph 图片

**本月 (Month 1)**:
9. 实现标签云和分类
10. 集成 Lunr.js 搜索
11. 添加评论系统
12. 性能优化 (懒加载等)

---

## 📊 优化效果预期

**用户体验提升**:
- 移动端加载速度: 2s → 1.2s (40% 提升)
- Lighthouse 性能得分: 85 → 95
- 社交分享转化率: +30%
- RSS 订阅转化率: +50%

**内容质量提升**:
- 文章结构一致性: 100%
- 代码示例可读性: +80%
- 导航效率: +60%

---

**维护者**: AI 办公助手
**最后更新**: 2026-04-06
**文档版本**: 1.0
