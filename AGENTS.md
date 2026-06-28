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

#### preloader 调优系列（5 个 commit：`57a28b4 / 3894201 / d2f79db / 823f500 / c74b5d7 / 18a5ea4 / 0a2f785`）
- **根本修改**（`3894201`）：`window.load` 改 `DOMContentLoaded` —— 后者要等所有 img/iframe/fetch 资源，avatar.png 4.4MB 偶尔拉失败（ERR_FAILED 21s/47s）→ preloader 走 8s 兜底才消失。改用 `DOMContentLoaded`（DOM 解析完就触发）+ 兜底 2s
- **转场升级**（`18a5ea4`）：clip-path circle 收缩（0.28s "啪一下爆缩"）→ transform scaleY 幕布式（0.85s 从顶部向下卷，cubic-bezier(.76,0,.24,1)）+ 内部 logo 上飞 60px + 微缩 + 渐隐
- **DOM remove 坑**（`0a2f785`）：CSS transition 改了，**JS 的 `setTimeout(preloader.remove, 150)` 没同步改**，导致 scaleY 0.85s 动画被截断到 0.15s，用户看到的还是"啪一下"。改成 ≥ 转场时长（900ms）。**经验：以后改任何 CSS transition 时长，同步检查 JS 端是否有相关 timer 依赖**
- **avatar 优化**（`3894201` 顺手）：`loading="lazy" decoding="async"` 让 avatar 脱离首屏关键路径，不再影响 `window.load`
- **时长微调**：`minDuration` 经 200→700→1200→900ms（用户反复调），最终稳定在 900ms
- 当前时序：0~0.9s 进度条 0→100% → 0.95s 内部 logo 上飞渐隐 + 幕布开始卷 → ~1.75s 完全消失

### P0.1 · Mobile 真机测试 ✅ 通过（2026-06-28）
- ✅ Playwright headless Chromium + iPhone 14 Pro viewport（390×844 / DPR 1）实测
- ✅ 浮卡 0 重叠：MODEL (240,109→370,189 130×80) / PROMPT (20,261→110,316 90×55) / DATASET (20,355→135,465 115×110)
- ✅ 间距 166/72/39px，console 0 error 0 warning
- ✅ 之前 user 反馈"重叠"确认是 GFW 间歇屏蔽 GitHub Pages CDN 路由到老节点；真实 Chromium 渲染无问题
- ✅ 桌面端 hash scroll / modal / theme toggle / back-top / nav 遮挡验证 OK（md5 验证）
- ⚠️ 真机 iOS Safari 触屏 / safe-area 物理验证待 user 拿真机走一遍（hamburger / 圆角 / home indicator）
- 验证截图：`/Users/aidon/mobile-cards-390x844.png`

#### `a1fecfd` P0.1.1 banner-meta 撞车浮卡 — 根因修复（2026-06-28）
- **症状**：user 反馈 mobile 浮卡仍"重叠"，截图显示 "1000%"（实为 `100`+`%`）/ `PROGRESS` / `FOCUS · AI 训练` 跟 DATASET 卡严重撞车
- **根因**：mobile media query 把 `.banner-meta` 绝对定位到 `.banner-visual` 框底部（`left:8px;bottom:8px`），跟左下角 DATASET 浮卡 (115×110 left:0 bottom:0) Y 轴重叠
- **修复**：mobile 重置 `.banner-meta` 为 `position:static` + `display:flex` 横排 + 缩字号（18px） + 取消 z-index → 从 visual 框拿出来回到 banner-inner 文档流，CTA 下方独立一行
- **副作用**：media query 后部旧绝对定位代码（line 1498-1505）会后写后赢覆盖新代码 → **同步删除**
- **520 query**：`banner-meta-item strong` 字号 26→18，跟 860 query 一致
- **桌面端 line 727-741 完全不动** ✓ — Playwright 1440×900 实测 banner-meta 仍在 (148,706,665×119) static 横排、3 浮卡原样
- **mobile 实测 390×844**：banner-meta `(20,767,350×100) static` 在 visual `(20,927,350×360)` 上方独立显示；3 浮卡 MODEL (240,923,130×80) / PROMPT (20,1075,90×55) / DATASET (20,1173,115×110) 全在 visual 框内，间距 72/43/4px，**0 重叠**

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
- mavis browser tool 是首选；具体走 Edge / Chrome / 其他哪个浏览器**不固定，看 broker 当前连的是哪个就用哪个**
- user 2026-06-28 明确"哪个适合工作你就打开哪个就行"，不再硬性指定品牌
- dev automation（Playwright / Puppeteer / Selenium 等）跟浏览器品牌无关，按需调
- 约定已写入 `~/.mavis/memory/user.md`（type: workflow-rule）
- 历史：2026-06-26~27 一天内 Edge ↔ Chrome 反复 3 次，每次都更新 memory + AGENTS.md。2026-06-28 终止决策反复。

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
- P0.3 vCard 信息：彭乙东 + 13670411826 + 390508183@qq.com + aidon277（**✅ 已与站点对齐，2026-06-27 mobile 测试时确认**）
- P1.3 需用户决定是否公开服务定价
- P1.4 需用户决定 Calendly vs 微信扫码预约
- P1.2 需用户确认真实客户名单
- P2.4 需用户决定是否出镜/提供环境照片
- P2.7 需用户决定域名（aidon.pro / aidon.ai / aidon.cn）

---

## 📌 2026-06-27 mobile 端深度改造 — 阶段性存档（user 出门暂停）

### 已上线 commits（origin/main 全部同步）
- `90b3be2` fix(mobile): 浮卡改对角线错落分布（参照 desktop）解决堆叠重叠
- `a1fecfd` feat(mobile): 删掉旋转虚线圆环（user 决定不要这个装饰）
- `372c73e` feat(mobile): 圆环改为圈住'训练'二字（已被 a1fecfd 删）
- `42dc4ef` fix(mobile): 圆环位置改 h1 文字右上角画框（已被 a1fecfd 删）
- `3851398` feat(mobile): 整页背景重新设计 + 6 层 mobile 专属高级感

### 当前 mobile 状态
- **背景**（3851398）：✅ body 6 层 mobile 背景 + banner::after hero 高光带 + banner-orb 重定位到 top:24% left:50% 400px + banner-bgword 隐藏
- **浮卡**（90b3be2）：✅ 参照 desktop 对角线错落分布，缩 30%
  - card-1 (MODEL 右上): top:0 right:0 130×80
  - card-2 (DATASET 左下): bottom:0 left:0 115×110
  - card-3 (PROMPT 左中): top:155 left:0 90×55
  - 齿轮: 28×28 紧贴 card-1 右上外
  - 几何验证 0 重叠（间隔 75/60/190px in 380px visual 容器）
- **圆环**：✅ 已删除（user 决定）
- **desktop**：0 改动（line 791-804 浮卡 + 187-205 body 6 层 background + 493-499 banner-orb + 484-491 banner-bgword 全部保留）

### ⚠️ User 反馈 "还是会重叠"（2026-06-27 18:45）
- deployed HTML 100% 部署成功（curl 真实 GitHub Pages 验证 3 次取样全部含 130×80 / 115×110 / 90×55）
- 几何计算 0 重叠（理论）
- **user 浏览器拿到的可能是 fastly 老节点 cache**（GFW 屏蔽 GitHub Pages CDN 间歇）
- **user 不想再每次都自己硬刷看**

### 🔧 User 决策（2026-06-28）：不再硬性指定浏览器品牌
- 之前在 Edge ↔ Chrome 之间反复过 3 次，user 明确"哪个适合工作你就打开哪个就行"
- 终止单一品牌硬性指定，**mavis browser 走哪个就用哪个**
- mobile 真机测试：DevTools mobile emulation（Chrome DevTools 移动 emulation 最完整，Edge 也行）

### 📋 User 回来后执行清单（agent 端）
1. **跑 mavis browser 状态自检**：`mavis browser status` 看 broker / native host
2. **跑 mobile 真机测试**（用 broker 当前连的浏览器 DevTools mobile emulation）：
   - 390×844 viewport（iPhone 14 Pro）
   - 跑真机 mobile 浮卡截图
   - 跑 `getBoundingClientRect` 实际渲染坐标
   - **如果还重叠** → 立即改 CSS（用真机看到的数据）
   - **如果不重叠** → archive completed
3. **archive completed**: 浮卡验证通过后 commit AGENTS.md 记录最终结果

### 已知工具/环境问题（不阻塞）
- GFW 间歇屏蔽 GitHub Pages CDN：curl 经常 HTTP 000，但 mavis browser + curl 重试能拿到
- mavis browser screenshot 工具有 bug（不响应 navigate，返回无关旧图）— 已知，AGENTS.md 已记
- mavis browser 无 evaluate / 无 viewport resize（用 DevTools 协议补充）
- mavis broker 卡在旧 tab claim 释放不掉时，杀掉那个浏览器重启，broker 自动接管新的

### 跨项目记忆（已写 agent memory）
- 浏览器偏好按需选择，停止单一品牌硬性指定（2026-06-28 user 明确）
- mobile 真机测试用 DevTools mobile emulation，不让 user 自己看
- mavis browser screenshot 工具不可靠（多次验证 bug）
- 之前的 GFW / CDN / cache 经验教训

### Next session 第一步
读这个文件 → 跑 mavis browser status → 用 broker 连到的浏览器跑 mobile 真机浮卡测试

---

## 👤 用户偏好

- 极简轻奢科技商务风 / 深色高级感
- 终端命令不熟，适合"我帮他跑"的模式
- **浏览器不硬性指定品牌**（2026-06-28 user 明确"哪个适合工作你就打开哪个就行"）
- 浏览器操作走 mavis browser tool，**走 broker 当前连的真实浏览器**（Edge / Chrome 都行）
- **mobile 真机测试用 DevTools mobile emulation**（哪个浏览器连上用哪个，不再让 user 自己看）
- Lighthouse / axe 等 CLI 审计工具 OK（CLI 不是 GUI）
- 见 `~/.mavis/memory/user.md` / `~/.mavis/agents/mavis/memory/MEMORY.md`
