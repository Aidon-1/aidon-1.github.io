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

## 今日完成（2026-06-26）

接 2026-06-25 计划，P0 + P1 全部交付（commit `6e5258e` → `ec0e516` → 当前）：

### P0 · 必做（全 4 项 ✅）
- **P0.1 Mobile 真机测试 + 修复** —— Playwright Chromium 跑 360/390/768 三个 viewport，修了 2 个 bug：
  - about 头像区 mobile：mark 圆从 64→48px，"彭乙东" pill 从 18→14px，caption 9.5px（避免遮挡人物 + TEMP COFFEE 招牌）
  - 360px 下 banner 标题断字：accent 加 `nowrap` + h1 字号 36px 适配（"跨界复合型 AI 训练师" 一行容下）
  - **bug 笔记**：mobile 修复被 base 样式覆盖了一次（CSS 顺序问题），把 media query 移到 base 之后才生效
- **P0.2 滚动条 themed** —— 早就用 `var(--c-accent)` 渐变 + glow，自动随 dark/light 主题切换
- **P0.3 回顶按钮** —— fixed bottom-right，滚 800px 浮出，glass + accent gradient hover，prefers-reduced-motion 兜底
- **P0.4 SEO meta + favicon + og:image** —— 全套：
  - head：keywords / author / robots / canonical / theme-color (双模式)
  - Open Graph 完整 6 项 + Twitter Card `summary_large_image`
  - **favicon.svg** —— 渐变蓝紫方块 logo
  - **og-image.svg** —— 1200×630 品牌分享卡
  - JSON-LD Person 结构化数据

### P1 · 内容深化（全 4 项 ✅）
- **P1.5 Contact form 真实化** —— 4 字段（姓名/邮箱/话题/留言）走 Web3Forms API（access_key 占位 `YOUR_WEB3FORMS_ACCESS_KEY`，未配置时回退到 mailto 提示）
  - 状态三态：loading spinner / success / error
  - 前端必填 + 邮箱格式二次校验（mobile safari 兜底）
  - 表单暗色主题匹配 contact-info 卡，accent focus ring
- **P1.6 service-card sweep** —— 早就做完，6 个 service-card 全部 `has-sweep` + `.card-sweep`
- **P1.7 Blog 加 2 篇深度文**（代写，9 篇总数）：
  - 08 CASE STUDY: 项目复盘：4 周帮电商店铺搭出 AI 客服模型
  - 09 FRAMEWORK: 思维方法：把 AI 训练当投资组合管理
- **P1.8 CTA 文案打磨**（A 方案：务实商务）：
  - 主 CTA：`了解主业服务` → `了解训练服务`
  - 次 CTA：`商务合作` → `商务洽谈`
  - Quick card #5：同步改 `商务洽谈`

### 浏览器链路
- mavis browser bridge（Edge 真实）已 connected
- native host 5 个浏览器全注册（Edge 路径已生效）
- 强制约定：以后所有浏览器相关操作走 mavis browser tool → 真实 Edge，**禁调 Playwright/Puppeteer 等 headless Chromium**
- 约定已写入 `~/.mavis/memory/user.md`（type: workflow-rule）

## 明日优化计划（2026-06-27）

### P2 · 体验 / 可访问性
1. **A11y 增强** —— focus ring 可见 / skip-link / aria 标签
2. **prefers-reduced-motion 全局生效**（部分动画未覆盖）
3. **Lighthouse 跑分**（Performance/SEO/Accessibility）

### P3 · 长线
4. JS 模块化（2900+ 行单文件）
5. 案例/作品详情页（多页结构）
6. 真实图片/视频（替代 CSS 装饰）

### 维护性 TODO
- Web3Forms access_key 待用户去 web3forms.com 注册填入（现在是占位）

## 用户偏好

- 极简轻奢科技商务风 / 深色高级感
- 终端命令不熟，适合"我帮他跑"的模式
- **默认浏览器：Microsoft Edge**（不要 Chrome/Chromium，包括 Playwright 这类 headless automation）
- 见 `~/.mavis/memory/user.md`