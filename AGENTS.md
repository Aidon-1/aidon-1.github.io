# AGENTS.md — aidon-1.github.io

彭乙东 AI 训练师个人品牌站。GitHub Pages 部署。

## 项目概览

- **仓库**: https://github.com/Aidon-1/aidon-1.github.io
- **部署**: GitHub Pages（main 分支直接发布）
- **形式**: 单文件 SPA（`index.html`，~2700 行 HTML + 内联 CSS + 内联 JS）
- **设计风格**: 极简深色高级感 / 蓝紫 accent
- **Mobile-first responsive**（PC 优先优化）

## 文件结构

```
.
├── index.html              # 全部代码（HTML + CSS + JS 单文件）
├── assets/                 # 静态资源
└── AGENTS.md               # 本文件
```

## 关键章节 ID

`#home` `#about` `#service` `#career` `#qualification` `#blog` `#resources` `#contact`

## 今日完成（2026-06-25）

11 个 commit，主题切换 → 背景升级 → preloader → 卡片 sweep → 光球 → 电路板 → 5 微调 → count-up + nav sticky。

详见 git log。

## 明日优化计划（2026-06-26）

### P0 · 必做
1. **Mobile 真机测试 + 修复**（所有测试都是 desktop viewport）
2. **滚动条 themed**（webkit-scrollbar 配色统一 dark/light）
3. **回顶按钮**（滚 800px 后右下角浮出，点击回顶）
4. **SEO meta + favicon + og:image**

### P1 · 内容深化
5. **Contact form 真实化**（现在是 mailto 还是 form？）
6. **service-card 同步 sweep 动效**（和 geom-card 一致）
7. **Blog section 加 1-2 篇真实文章**（用户写稿）
8. **CTA 文案打磨**

### P2 · 体验 / 可访问性
9. **A11y 增强**（focus ring / skip-link / aria）
10. **prefers-reduced-motion 全局生效**
11. **Lighthouse 跑分**（Performance/SEO/Accessibility）

### P3 · 长线
12. JS 模块化（2700+ 行单文件）
13. 案例/作品详情页（多页结构）
14. 真实图片/视频（替代 CSS 装饰）

## 用户偏好

- 极简轻奢科技商务风 / 深色高级感
- 终端命令不熟，适合"我帮他跑"的模式
- 见 `~/.mavis/memory/user.md`