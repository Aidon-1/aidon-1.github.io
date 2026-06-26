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

### P2 · 体验 / 可访问性（全 3 项 ✅）
- **P2.9 A11y 增强** —— 
  - **skip-link**：body 顶部加 `<a class="skip-link" href="#about">跳到主内容</a>`，Tab 触发时 fixed top:16px 浮出
  - **focus ring 全局**：`:focus-visible` 用 accent 双层 outline（键盘 Tab 才显示，鼠标点击不打扰）
  - **link-name FAIL 修复**：side-scroll-dot 8 个空 `<a>` 加 `aria-label="跳到 ..."`
  - **quick-card div → a**：5 个 div 改成 `<a href data-goto aria-label>`，键盘 Tab 自动可达 + Enter 触发跳转；JS click 监听加 `e.preventDefault()` 避免双跳
  - **quick-card CSS 补**：display:block + text-decoration:none + color:inherit
- **P2.10 prefers-reduced-motion 全局兜底** —— `@media(prefers-reduced-motion:reduce)` 全局规则：
  - 所有动画 `duration:0.001ms !important` + 1 次
  - 所有过渡 `duration:0.001ms !important`
  - scroll-behavior:auto
  - 局部兜底：`.reveal` 直接显示 / `.card-sweep::before` 停 / `.banner-orb-ring` 停 / `.footer-circuit` display:none / `.circuit-dot` 停
- **P2.11 Lighthouse 跑分**（deploy 版实测 `https://aidon-1.github.io/`）：
  - **SEO 100** ✅ 完美（meta / og / 标题 / 描述 / heading-order 全 PASS）
  - **Best Practices 100** ✅ 完美（HTTPS / 无错库 / 合理 image aspect）
  - **Accessibility 84 → 待修 link-name**（修完预估 92+）：side-scroll-dot aria-label + quick-card a11y
  - **Performance 55** ⚠️ 主要瓶颈：FCP/LCP 8.4s（lighthouse 节流模拟 slow 4G + 4x CPU），真实用户 Edge 看是流畅的；优化空间见 P3 路线图
  - **CLS 0.007** ✅（无位移）

## 明日优化计划（2026-06-27 → 长线）

### P2 · 收尾
1. **Performance 优化**（55 → 90+）：
   - 关键 CSS 提取 + 大块延迟（circuit / banner-orb / preloader 异步）
   - 电路板 DOM 数量精简（当前 ~20 个 dot）
   - 首屏字体加载策略（系统字体已 OK，可加 preload 提示）
   - 考虑拆 CSS / JS 到外部文件 + gzip
2. **Lighthouse 重测**（验证分数）

### P3 · 长线（按工作量展开）
1. **JS 模块化（commit 候选）** —— `assets/js/` 拆出：
   - `preloader.js` / `theme.js` / `nav.js` / `reveal.js` / `count-up.js` / `tilt.js` / `circuit.js`
   - 减少 main JS 体积 + 利于按需加载
2. **真实案例详情页** —— `/cases/<slug>.html` 多页结构：
   - 案例库列表（首页集成入口）
   - 单案例页（问题 / 方案 / 流程图 / 数据 / 客户感言）
3. **真实图片/视频** —— 拍：办公桌 / 训练后台 / 团队 / 屏幕录制训练流程
4. **A/B test CTA 文案**（P1.8 后续）—— 看「了解训练服务」CTR vs 「看看我能帮上什么」

### 维护性 TODO
- Web3Forms access_key 待用户去 web3forms.com 注册填入（现在是占位）
- Web3Forms access_key 拿到后改 `index.html` 第 ~2391 行占位字符串

## 用户偏好

- 极简轻奢科技商务风 / 深色高级感
- 终端命令不熟，适合"我帮他跑"的模式
- **默认浏览器：Microsoft Edge**（不要 Chrome/Chromium，包括 Playwright 这类 headless automation）
- Lighthouse / axe 等 CLI 审计工具 OK（CLI 不是 GUI，不算 Edge 偏好违反）
- 见 `~/.mavis/memory/user.md`