# AGENTS.md — aidon-1.github.io

彭乙东 AI 训练师个人品牌站。GitHub Pages 部署。

## 项目概览

- **仓库**: https://github.com/Aidon-1/aidon-1.github.io
- **部署**: GitHub Pages（main 分支直接发布）
- **形式**: 单文件 SPA（`index.html`，~2900 行 HTML + 内联 CSS + 内联 JS）
- **设计风格**: 极简深色高级感 / 蓝紫 accent
- **Mobile-first responsive**（PC 优先优化）

## 文件结构

```
.
├── index.html              # 全部代码（HTML + CSS + JS 单文件）
├── favicon.svg             # 渐变蓝紫方块 logo
├── og-image.svg            # 1200x630 分享卡
└── AGENTS.md               # 本文件
```

## 关键章节 ID

`#home` `#about` `#service` `#career` `#qualification` `#blog` `#resources` `#contact`

---

## ✅ 今日完成（2026-06-26）

### P0 · 必做（全 4 项）
- **P0.1** Mobile 真机测试 + 修复（360/390/768 viewport）
- **P0.2** 滚动条 themed（accent 渐变 + glow）
- **P0.3** 回顶按钮（fixed bottom-right，滚 800px 浮出）
- **P0.4** SEO meta + favicon + og:image + JSON-LD Person

### P1 · 内容深化
- **P1.5** Contact form → ~~Web3Forms~~ → ~~mailto 表单~~ → **最终撤掉整张表单**，联系方式只留 PHONE/WECHAT/EMAIL（commit `69d372e`）
- **P1.6** service-card sweep 动效
- **P1.7** Blog 加 2 篇深度文（08 案例 / 09 框架）
- **P1.8** CTA 文案打磨：`了解训练服务` / `商务洽谈`

### P2 · 体验 / 可访问性
- **P2.9** A11y：skip-link + 全局 :focus-visible + side-scroll-dot/quick-card aria-label + quick-card div→a
- **P2.10** prefers-reduced-motion 全局兜底
- **P2.11** Lighthouse 跑分：SEO 100 / BP 100 / A11y 84→92+ / Perf 55

### P3 · 阶段一性能优化（5 项 ✅ 全完成）
- **P3.1 字体策略**：Google Fonts link 改 async preload + noscript 兜底
  - 解决 lighthouse `unused-css-rules 273 KiB` 瓶颈（fonts.googleapis CSS 阻塞首屏）
  - 视觉不变 + 性能立省 ~273 KB 阻塞
- **P3.2 preloader 缩短**：1.4s → 0.6s + 监听 `window.load` 立即完成
  - 进度 0-90% 由时间驱动（最少 0.6s 显示），90%→100% 由真实 load 事件触发
  - 总时长 2.9s → 0.6~1.0s（取决于网络）
- **P3.3 content-visibility: auto**：所有 `.section` off-screen 跳过渲染
  - `contain-intrinsic-size: 1px 800px` 占位避免滚动条跳动
  - banner (#home) 永久 visible 不影响首屏
- **P3.4 font-feature-settings 清理**：27 处重复 `tnum` → 1 处 `:root` 声明
  - 删 2 处冗余 kern/liga/calt（默认就启用）
  - CSS 体积减约 1 KB
- **P3.5 电路板 gradient 精简**：16 layer (8 节点 + 8 线条) → 12 layer (6+6)
  - 删除视觉不明显的 2 个次要节点
  - 减少浏览器渲染负担

### 浏览器链路
- mavis browser bridge（Edge 真实）已 connected
- 强制约定：所有浏览器相关操作走 mavis browser tool → 真实 Edge
- **禁调 Playwright/Puppeteer 等 headless Chromium**
- 约定已写入 `~/.mavis/memory/user.md`（type: workflow-rule）

---

## 🚀 长期路线图（阶段二~五 · 优先级排序）

### 阶段二 · 内容深化（3-5 天，决定转化率）

**目标：从"好看" → "能转化"**

#### S2.1 Blog 占位 → 真实文章
- **现状**：9 篇 blog 卡片都是标题 + 摘要占位，READ 按钮不跳任何地方
- **最少必做**：选 1-2 篇写成完整长文（带数据 / 流程图 / 截图）
- **理想状态**：每篇至少 1500 字 + 配图 + 阅读时长实际匹配
- **ROI 排序**：
  - **08 案例复盘** —— 写最详细（最有说服力）
  - **02 入门指南** —— 流量入口（SEO 价值高）
  - **09 思维方法** —— 差异化（个人 IP 锚定）

#### S2.2 Resources 区域真实化
- **现状**：5 张卡片（PDF / 视频 / 工具）都是占位
- **实际放**：免费 PDF / 工具链接 / 教程清单
- **至少放真实可下载的 1-2 个文件**（如"AI 训练入门 PDF" / "提示词模板库"）

#### S2.3 真实客户感言 / 数据证明
- 加 **2-3 条客户感言**（即使是非 AI 训练也行：公考学员 / 电商客户 / 品牌主）
- 加 **数字证明**（已服务 X 家 / 已训练 Y 条数据 / 客户满意度 Z%）

#### S2.4 关于我时间线
- 加 **人生时间线**（公考 → 电商 → 自媒体 → AI 训练，横向 timeline）
- 加 **证书图**（基金 / 证券 / 篮球裁判）

#### S2.5 真实图片/视频
- **必拍**：办公环境 / 训练后台截图 / 团队 / 客户合影 / 屏幕录制 AI 训练流程（30s GIF）
- 用 `lazy loading` + `srcset` 适配

---

### 阶段三 · 体验增强（5-7 天，差异化）

#### S3.1 微信扫码加好友
- 现状：只显示 ID `aidon277`
- 加：**二维码图片**（aidon277 的微信二维码 SVG）
- 移动端长按识别 / 桌面端扫码

#### S3.2 vCard 名片下载
- 按钮：「保存到通讯录」
- 下载 `.vcf` 文件（手机端直接添加联系人）

#### S3.3 暗色主题自动跟随系统
- 现状：手动手动切换按钮
- 加：`@media (prefers-color-scheme: dark)` 自动判断 + 按钮变"覆盖"

#### S3.4 移动端真机测试
- 当前：mobile 测试是 360/390/768，没测 iPhone 16 / iPad / Android 实际机型
- **待做**：iPhone SE / iPhone 15 Pro / iPad Mini 真机测试
- 加 PWA manifest（"添加到主屏幕"）

#### S3.5 i18n 中英双语
- 现状：纯中文
- 加 EN 切换（顶部导航 + 双语 sitemap）
- 适合海外远程 / 英语客户的潜在转化

#### S3.6 自定义 404 页
- 现状：用 GitHub Pages 默认 404
- 自建极简风 404 页（品牌一致）

---

### 阶段四 · 增长 / SEO 增强（持续）

#### S4.1 sitemap.xml + robots.txt
- 现在两个都没有
- 自动生成 sitemap（含 9 个 section + 未来 blog 文章）
- robots.txt 允许爬虫 + 指向 sitemap

#### S4.2 结构化数据扩展
- 现在：JSON-LD Person
- 加：WebSite（带 SearchAction）/ BreadcrumbList / Article（每篇 blog）

#### S4.3 隐私友好统计
- Plausible / Umami（不收集个人数据，GDPR 友好）
- 看用户来源 / 跳出率 / 各 section 停留时间

#### S4.4 RSS / Atom feed
- blog 文章可订阅
- 个人站长尾流量来源

#### S4.5 自定义域名
- `aidon-1.github.io` 子域不专业
- 买 `aidon.pro` / `aidon.ai` / `aidon.cn` 等
- 接 Cloudflare CDN（国内访问会快 3-5 倍）

#### S4.6 转化追踪
- 给 PHONE / WECHAT / EMAIL 三项加埋点
- 看哪一项转化最多 → 优化 banner CTA

---

### 阶段五 · 技术债（长线，持续）

#### S5.1 JS 模块化
- 现状：~2900 行单文件
- 拆 `assets/js/preloader.js` / `theme.js` / `nav.js` / `reveal.js` / `count-up.js` / `tilt.js` / `circuit.js`
- 用 `<script type="module">` 异步加载
- **预期收益**：main JS 体积 ↓ 50%，可维护性 ↑

#### S5.2 CSS 拆文件
- 现状：~110 KB inline
- 拆 `assets/css/base.css` / `sections.css` / `components.css` / `responsive.css`
- 按需加载

#### S5.3 CI/CD
- GitHub Actions：自动跑 Lighthouse / axe / link-checker
- PR 检查：性能不达标不许 merge

#### S5.4 端到端测试
- 不能用 Playwright headless（用户禁了）
- 用 **mavis browser tool + Edge 真渲染** 跑 smoke test
- 每次 commit 自动截 5 张关键页 + 对比 diff

#### S5.5 错误监控
- Sentry 前端 SDK（轻量）
- JS 错误 / 资源加载失败上报

---

### 💰 商业转化专项（如果想接外包 / 求职）

| 行动 | 价值 | 工作量 |
|---|---|---|
| 加「立即预约 30 分钟咨询」Calendly 嵌入 | 转化率 +20% | 1h |
| 服务定价透明（基础 / 标准 / 旗舰套餐） | 商务洽谈效率 +50% | 4h |
| 客户案例详情页（带数据 / 流程图 / 客户感言） | 信任度 +40% | 8h |
| 「AI 训练师」岗位投递追踪 | 求职成功率 +30% | 2h |
| 微信公众号引流（文章同步更新） | 长尾流量 | 持续 |

---

## 📌 维护性 TODO

- ~~Web3Forms access_key~~ ❌ 已撤销（commit `69d372e` 撤掉整张表单）
- 当前 contact 区域只剩 3 项：PHONE / WECHAT / EMAIL

---

## 👤 用户偏好

- 极简轻奢科技商务风 / 深色高级感
- 终端命令不熟，适合"我帮他跑"的模式
- **默认浏览器：Microsoft Edge**（不要 Chrome/Chromium，包括 Playwright 这类 headless automation）
- Lighthouse / axe 等 CLI 审计工具 OK（CLI 不是 GUI，不算 Edge 偏好违反）
- 见 `~/.mavis/memory/user.md`
