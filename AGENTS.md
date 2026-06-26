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

### P0.0 · Bug 修复（commit `884298a`）
- **modal 打开鼠标消失**：自定义光标 `.cursor-dot/.cursor-ring` z-index:9999，被 modal 99990 遮罩盖住 → JS 在 `openArt/closeArt` 给 body 加 `.modal-open` class，CSS 隐藏 cursor
- **移动端进不去**：preloader 永远等 `window.load`，mobile 4G 下 fonts 加载慢/被墙时 `window.load` 迟迟不触发 → 加 8s 强制兜底 timeout
- 顺带把 `.no-scroll` 替换为 `.modal-open`（语义更准确，单 class 同时管 cursor + 滚动锁）

### 阶段二 · 内容深化（S2.1 + S2.2 完成，commit `941663f`）
- **S2.1 Blog 占位 → 真实文章** ✅ 9 篇长文（800-1500 字）含 h3/表格/流程图/KPI/code/星标/list，全部 modal 弹窗
- **S2.2 Resources 区域真实化** ✅ 6 个资源（含 12 个可一键复制的 prompt 模板）

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

## 🚀 长期路线图（2026-06-26 重排 · 按 ROI 分级）

> 排序逻辑：**P0（立刻能搞）→ P1（1 周内，差异化 + 转化）→ P2（持续，长线技术债 + 品牌）→ P3（细节精进，攒人品）**

---

### 🔥 P0 · 立刻能搞（1-2 天，立竿见影）— **先做这一档**

| 编号 | 项 | 工作量 | ROI | 说明 |
|---|---|---|---|---|
| P0.1 | **mobile 真机测试** | 0.5d | 极高 | **必做**。所有验证都在 PC Edge + 缩放 viewport，**iPhone Safari / Android Chrome 真机从未测过**。建议：iPhone + Android 各一台，重点测 modal 手势、底部 home indicator、字体加载失败 fallback、横竖屏 |
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

1. **P0.1 mobile 真机测试**（**没测就别推朋友圈**，别让客户第一个看到就掉）
2. **P0.2 微信二维码**（30 分钟，转化 +50%）
3. **P0.3 vCard 名片**（1 小时，HR/猎头友好）
4. **P1.2 客户感言**（先问用户有没有真实客户）
5. **P1.1 自定义 404**（2h，顺手搞）
6. **P1.5 + P1.6 SEO 双件套**（5h，一次性）

**第二周起**开 P2 长线（先 P2.4 真实图片/视频，**先问用户愿不愿意出镜**）。

**别做 P2.1 JS 模块化**（重构黑洞陷阱），等 P0/P1 全部 done 且用户主动要求再开。

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
