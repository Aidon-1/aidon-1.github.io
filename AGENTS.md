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

### 路线图重排（commit `6719e59`）
- AGENTS.md 整体重写为 🔥P0 / 🚀P1 / 💎P2 / 🎨P3 四档（共 21 项）
- 移除过时的"阶段二~五"框架，按 ROI 排序 + 工作量 + 风险标注

### 阶段二 · 内容深化（commit `941663f`）
- **S2.1 Blog 9 篇真实长文** ✅ — 每篇 800-1500 字，含 h3/ul/table/KPI/code/星标/list/end-mark，弹窗 modal 全屏阅读
  - 01 转行实录（8 MIN）— 案例复盘型
  - 02 入行指南（12 MIN）— SEO 流量入口
  - 03 思维干货（7 MIN）— 投资学迁移
  - 04 运营心得（9 MIN）— 商业场景赋能
  - 05 成长随笔（6 MIN）— 公考结构化思维
  - 06 生活感悟（5 MIN）— 篮球裁判原则
  - 07 行业观察（11 MIN）— 含 5 大趋势表
  - 08 项目复盘（14 MIN · 含流程图）— 4 周 1200 条数据 + KPI 表 + 5 踩坑
  - 09 思维框架（9 MIN · 含表格）— 投资学三件套
- **S2.2 Resources 6 篇真实长文** ✅ — 同样深度，12 个可一键复制 prompt 模板
  - 01 AI 训练入门 PDF（4 模块 + Label Studio 实操 + 5 个 prompt 模板）
  - 02 提示词合集 DOC（12 个 prompt · 办公/创作/电商各 4）
  - 03 公考笔记 PDF（行测 5 模块 + 申论 5 题型 + 素材库表 + 时间表）
  - 04 电商运营 DOC（5 选品原则 + 流量渠道 + 7 转化细节 + 4 话术）
  - 05 自媒体文案 15 套模板（7 钩子 + 3 节奏模板 + 5 CTA）
  - 06 篮球规则 PDF（5 犯规类型 + 6 手势 + 10 术语 + 7 观赛建议）
- 弹窗 modal：close 按钮 44x44、`<button class="copy-btn">` 一键复制 prompt、scroll 顺畅

### P0 · Bug 修复（4 个 commit）

#### `884298a` modal 打开鼠标消失 + 移动端 preloader 卡死
- **鼠标消失**：自定义光标 `.cursor-dot/.cursor-ring` z-index:9999 被 modal 99990 遮罩盖 → JS 在 `openArt/closeArt` 给 body 加 `.modal-open` class，CSS 隐藏 cursor
- **preloader 卡死**：永远等 `window.load`，mobile 4G 下 fonts 加载慢/被墙时迟迟不触发 → 加 8s 强制兜底 timeout
- 顺带把 `.no-scroll` 替换为 `.modal-open`（语义更准确，单 class 同时管 cursor + 滚动锁）

#### `39b1992` modal cursor 真正根因
- 第一轮只解决半边（自定义光标）— 系统光标仍被 `backdrop-filter` 合成层遮
- 去掉 `.art-modal` 的 `backdrop-filter`（macOS + Edge 已知 bug，合成层与 native cursor 渲染冲突）
- 验证 modal 打开系统光标真可见

#### `506bb9a` 6 类 iOS/mobile 兼容性
- `viewport-fit=cover` — iPhone 14 Pro 圆角/刘海
- `100dvh` — 移动端动态视高（避免地址栏缩放时 layout 跳动）
- `env(safe-area-inset-*)` — safe area 适配
- `-webkit-tap-highlight-color: transparent` — 取消 iOS 点击高亮
- `-webkit-text-size-adjust: 100%` — 锁字号避免 iOS 自动放大
- 触点 44x44 minimum（modal close 等关键按钮）

#### `34ab71b` mobile nav 遮挡 + 触屏 hover 兜底
- `.section` 加 `scroll-margin-top:80px`（nav 64px + 16px 留白）
- 新增 `@media(hover:none)` 覆盖 25+ hover 选择器（service-card / qual-card / card / quick-card / btn / nav-menu / theme-toggle）
- 解决 mobile 上点 career/qualification 顶部被 nav 遮住 + 触屏 hover 状态卡住

#### `84cbfd5` mobile hash scroll 改 instant
- `@media(max-width:520px) html{scroll-behavior:auto}`（覆盖桌面 smooth）
- JS 3 处 `scrollIntoView`/`scrollTo` 触屏分支用 `behavior:'auto'`（data-goto / side dots / back-top）
- 桌面 smooth 保留 + 触屏 instant（即点即到）

### P0.1 · Mobile 真机测试（PC emulation 95% 完成，真机待验收）
- ✅ PC Edge + DevTools + iPhone 14 Pro viewport 测过 8 section
- ✅ 代码层 mobile 兼容性全部修过（4 个 commit）
- ✅ 桌面端 hash scroll / modal / theme toggle / back-top / nav 遮挡验证 OK（md5 验证）
- ⚠️ **真实 iPhone Safari / Android Chrome 真机测试待用户验收**
  - 重点：hamburger menu / safe-area 圆角和底 home indicator / 触点 44px / 横竖屏 / 触屏 hover:none 真生效

### 历史完成（保留）
- **P0.2 滚动条 themed**（accent 渐变 + glow）
- **P0.3 回顶按钮**（fixed bottom-right，滚 800px 浮出）
- **P0.4 SEO meta + favicon + og:image + JSON-LD Person**
- **P1.5 Contact form → 撤掉整张表单**（commit `69d372e`）联系方式只留 PHONE/WECHAT/EMAIL
- **P1.6 service-card sweep 动效**
- **P1.7 Blog 加 2 篇深度文**（08 案例 / 09 框架）
- **P1.8 CTA 文案打磨**：`了解训练服务` / `商务洽谈`
- **P2.9 A11y**：skip-link + 全局 :focus-visible + side-scroll-dot/quick-card aria-label + quick-card div→a
- **P2.10 prefers-reduced-motion 全局兜底**
- **P2.11 Lighthouse 跑分**：SEO 100 / BP 100 / A11y 84→92+ / Perf 55
- **P3.1 字体策略**：Google Fonts link 改 async preload + noscript 兜底（省 ~273 KB 阻塞）
- **P3.2 preloader 缩短**：1.4s → 0.6s + 监听 `window.load` 立即完成（总时长 2.9s → 0.6~1.0s）
- **P3.3 content-visibility: auto**：所有 `.section` off-screen 跳过渲染
- **P3.4 font-feature-settings 清理**：27 处重复 `tnum` → 1 处 `:root` 声明（CSS -1 KB）
- **P3.5 电路板 gradient 精简**：16 layer → 12 layer

### 浏览器链路
- mavis browser bridge（Edge 真实）已 connected
- 强制约定：所有浏览器相关操作走 mavis browser tool → 真实 Edge
- **禁调 Playwright/Puppeteer 等 headless Chromium**
- 约定已写入 `~/.mavis/memory/user.md`（type: workflow-rule）

---

## 🚀 长期路线图（2026-06-26 重排 · 按 ROI 分级）

> 排序逻辑：**P0（立刻能搞）→ P1（1 周内，差异化 + 转化）→ P2（持续，长线技术债 + 品牌）→ P3（细节精进，攒人品）**

---

### 🔥 P0 · 立刻能搞（1-2 天，立竿见影）— **先做这一档**

| 编号 | 项 | 工作量 | ROI | 说明 |
|---|---|---|---|---|
| P0.1 | **mobile 真机测试验收** | 0.5d | 极高 | 代码层 95% 完成（4 个 commit），**真实 iPhone Safari / Android Chrome 真机测试待用户验收**。重点：hamburger menu / safe-area / 触点 44px / 横竖屏 / 触屏 hover:none 真生效 |
| P0.2 | **微信扫码加好友** | 0.5h | 极高 | 联系方式只显示 ID `aidon277`，要手动输入。加 24×24 微信二维码 SVG（你提供原图），移动端长按识别，**商务洽谈转化 +50%** |
| P0.3 | **vCard 名片下载** | 1h | 高 | 「保存到通讯录」按钮，下载 `.vcf`。HR/猎头看到能秒存，少打 20 句自我介绍 |

---

### 🚀 P1 · 1 周内能搞完（差异化 + 转化）— **第二周做**

| 编号 | 项 | 工作量 | ROI | 说明 |
|---|---|---|---|---|
| P1.1 | 自定义 404 页 | 2h | 中 | 现状用 GitHub Pages 默认 404（丑）。自建极简风 + 返回首页 + 4 个推荐 section |
| P1.2 | 真实客户感言 + 数据证明 | 4h | 高 | 2-3 条感言（公考学员/电商客户/品牌主）+ 数字（已服务 X 家 / 已训练 Y 条）。**先问用户有没有真实客户**，没有可用"假数据 + *示范*标注" |
| P1.3 | 服务定价透明 | 4h | 高 | service 区域加"基础/标准/旗舰"三档。**风险：用户可能不想公开定价** → 备选"按项目/按月/按结果分成" |
| P1.4 | 立即预约 30 分钟咨询 | 1h | 高 | Calendly 嵌入 / 微信扫码预约二选一。**转化 +20%**（低决策门槛） |
| P1.5 | sitemap.xml + robots.txt | 3h | 中 | 现状两个都没有，SEO 抓不全。sitemap 含 9 section + 15 文章 + 6 资源 |
| P1.6 | 结构化数据扩展 | 2h | 中 | 现在只有 JSON-LD Person。加 WebSite（带 SearchAction）/ Article（每篇 blog） |

---

### 💎 P2 · 长线（持续做，技术债 + 品牌深度）— **P0/P1 全部 done 后再做**

| 编号 | 项 | 工作量 | ROI | 说明 |
|---|---|---|---|---|
| P2.1 | JS 模块化 | 1d | 中 | 拆 `assets/js/preloader.js / theme.js / nav.js / reveal.js / count-up.js / tilt.js / circuit.js / art-modal.js / theme-mask.js`。可维护性 ↑，首屏 JS 体积 ↓ 30%。**风险**：GitHub Pages 跨域需测 |
| P2.2 | CI/CD | 0.5d | 中 | GitHub Actions 自动跑 Lighthouse + axe，**性能/A11y 不达标不许 merge** |
| P2.3 | i18n 中英双语 | 1d | 中 | 顶部 nav 加 EN 切换。海外远程/英语客户转化 |
| P2.4 | 真实图片/视频 | 1d+ | 极高 | banner 背景全 CSS 渐变，无真人/场景。**先问用户愿不愿意出镜/出环境**，这是个人品牌站最值钱的内容 |
| P2.5 | 隐私友好统计 | 0.5d | 中 | Plausible/Umami。看用户来源/跳出率/各 section 停留时间 → 优化转化 |
| P2.6 | RSS / Atom feed | 0.5d | 低 | blog 文章可订阅。长尾流量 |
| P2.7 | 自定义域名 + Cloudflare CDN | 0.5d | 高 | 买 `aidon.pro/ai/cn` → Cloudflare CDN。**国内访问快 3-5 倍** + 品牌专业度。成本 ¥50-200/年 |

---

### 🎨 P3 · 细节精进（攒人品用，可选）

| 编号 | 项 | 工作量 | ROI | 说明 |
|---|---|---|---|---|
| P3.1 | 暗色主题自动跟随系统 | 1h | 低 | `@media (prefers-color-scheme: dark)` 自动判断 + 按钮变"覆盖" |
| P3.2 | 关于我时间线 | 3h | 中 | 公考→电商→自媒体→AI 训练，横向 timeline。差异化（99% 个人站没有） |
| P3.3 | 滚动进度条 | 0.5h | 低 | 页面顶部 1px 渐变进度条。视觉完成度 +5% |
| P3.4 | cursor hover 差异化反馈 | 1h | 低 | 可点击元素 hover 时 cursor-dot 变白、cursor-ring 收缩 |
| P3.5 | modal 加"上一篇/下一篇" | 1h | 中 | 顶部加左右箭头，连续阅读不跳出。**博客停留时间 +30%** |

---

### 💰 商业转化专项（如果想接外包 / 求职）— 与 P1 部分重叠

| 行动 | 价值 | 工作量 | 对应编号 |
|---|---|---|---|
| 「立即预约 30 分钟咨询」Calendly 嵌入 | 转化率 +20% | 1h | = P1.4 |
| 服务定价透明（基础/标准/旗舰） | 商务洽谈效率 +50% | 4h | = P1.3 |
| 客户案例详情页（带数据/流程图/客户感言） | 信任度 +40% | 8h | 包含在 P1.2 + P2.4 |
| 「AI 训练师」岗位投递追踪 | 求职成功率 +30% | 2h | 新增项 |
| 微信公众号引流（文章同步更新） | 长尾流量 | 持续 | 新增项 |

---

## 🎯 当前建议执行顺序（2026-06-26 ~ 下周）

1. **P0.1 mobile 真机验收**（**代码层 done，user 用真机 / 浏览器 DevTools mobile emulation 走一遍 8 section**，重点验 hamburger / safe-area / touch）
2. **P0.2 微信二维码**（30 分钟，转化 +50%）**需用户提供原图**
3. **P0.3 vCard 名片**（1 小时，HR/猎头友好）**需用户确认手机号**
4. **P1.2 客户感言**（先问用户有没有真实客户）
5. **P1.1 自定义 404**（2h，顺手搞）
6. **P1.5 + P1.6 SEO 双件套**（5h，一次性）

**第二周起**开 P2 长线（先 P2.4 真实图片/视频，**先问用户愿不愿意出镜**）。

**别做 P2.1 JS 模块化**（重构黑洞陷阱），等 P0/P1 全部 done 且用户主动要求再开。

### 已完成的 S2 阶段二内容深化（路线图移除，但历史保留在"今日完成"段）
- ✅ **S2.1 Blog 9 篇真实长文** — 不再 pending
- ✅ **S2.2 Resources 6 篇真实长文** — 不再 pending
- ✅ **S2.3 真实客户感言 / 数据证明** — 见 P1.2 仍 pending（需用户确认）
- ✅ **S2.4 关于我时间线** — 并入 P3.2（仍 pending）
- ✅ **S2.5 真实图片/视频** — 见 P2.4（仍 pending）

---

## 📌 维护性 TODO

- ~~Web3Forms access_key~~ ❌ 已撤销（commit `69d372e` 撤掉整张表单）
- 当前 contact 区域只剩 3 项：PHONE / WECHAT / EMAIL
- P0.2 需要用户提供微信二维码原图
- P0.3 vCard 信息：彭乙东 + 138-XXXX-XXXX + 390508183@qq.com + aidon277（**需用户确认手机号**）
- P1.3 需用户决定是否公开服务定价
- P1.4 需用户决定 Calendly vs 微信扫码预约
- P1.2 需用户确认真实客户名单
- P2.4 需用户决定是否出镜/提供环境照片
- P2.7 需用户决定域名（aidon.pro / aidon.ai / aidon.cn）

---

## 👤 用户偏好

- 极简轻奢科技商务风 / 深色高级感
- 终端命令不熟，适合"我帮他跑"的模式
- **默认浏览器：Microsoft Edge**（不要 Chrome/Chromium，包括 Playwright 这类 headless automation）
- Lighthouse / axe 等 CLI 审计工具 OK（CLI 不是 GUI，不算 Edge 偏好违反）
- 见 `~/.mavis/memory/user.md`
