<div align="center">

# FUCK CLAUDE // 环境信号探测器

**估算浏览器环境中的“中国用户”信号**<br>
*Privacy-first browser signal estimator.*

[![Astro](https://img.shields.io/badge/Astro-7-FF5D01?style=for-the-badge&logo=astro&logoColor=white)](https://astro.build)
[![TypeScript](https://img.shields.io/badge/TypeScript-Strict-3178C6?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org)
[![Static](https://img.shields.io/badge/Output-Static-111111?style=for-the-badge)](https://docs.astro.build/en/basics/project-structure/)
![License](https://img.shields.io/badge/License-See%20repository-555555?style=for-the-badge)

</div>

---

## 01. THE PURPOSE // 项目本源

这是一个中英双语的本地浏览器检测工具，用于估算时区、语言、字体等环境信号是否呈现“中文环境”特征。检测逻辑不上传数据，也不发起网络请求。

[Repository](https://github.com/kerntau/fuckclaude)

## 02. CORE ARCHITECTURE // 核心架构

~~~mermaid
graph LR
  P[Browser APIs] --> D[Signal detectors]
  D --> S[Weighted score]
  S --> V[Verdict and matched signals]
  I[EN / ZH copy] --> V
  A[Astro build] --> HTML[Static dist]
~~~

页面可以读取操作系统时区、语言、Intl 区域设置、字体渲染和 UA 等浏览器可见信号；不能读取代理 hostname 或服务端配置，因此结果仅供参考。

## 03. TECHNICAL MATRIX // 技术矩阵

| 信号 | 权重 | 读取方式 |
| --- | ---: | --- |
| 系统时区 | 30 | Intl.DateTimeFormat |
| 浏览器语言 | 24 | navigator.language(s) |
| 中文字体 | 20 | Canvas 宽度探测 |
| Intl locale | 10 | Intl resolved locale |
| UTC+8 偏移 | 8 | getTimezoneOffset |
| Emoji 渲染提示 | 8 | 平台/UA 推断 |

分数区间为 Low 0–30、Medium 31–60、High 61–100。

## 04. REPOSITORY TOPOLOGY // 源码拓扑

~~~text
src/config/signals.ts       # 信号定义、权重和检测器
src/config/sponsors.ts      # 赞助商卡片数据
src/i18n/ui.ts              # 英文/中文文案
src/scripts/detect.ts       # 客户端扫描与打分
src/layouts/                # SEO 和全局样式
src/components/             # 扫描器、分数环、Mascot 等
src/pages/                  # / 与 /zh/ 页面
public/                     # 图片、图标与静态资源
scripts/gen-assets.mjs      # 图标/PWA/OG 资源生成
~~~

## 05. CLONE & QUICK START // 极速开始

需要 Node.js 18+ 和 pnpm。

~~~bash
git clone https://github.com/kerntau/fuckclaude.git
cd fuckclaude
pnpm install
pnpm dev
~~~

生产构建与预览：

~~~bash
pnpm build
pnpm preview
~~~

## 06. DEPLOYMENT & VERIFICATION // 部署与验证

将 dist/ 部署到任意静态托管。发布前在 astro.config.mjs 和 public/robots.txt 设置真实站点源；本项目不包含后端密钥。

运行 pnpm build 验证中英文路由、sitemap 和静态资源完整性。修改信号权重时应同步检查总权重仍为 100。

## 07. ENGINEERING CONTRACT // 工程契约

- 检测器保持纯客户端，不添加遥测或隐式数据上传。
- 信号名称、权重和阈值变更必须在 README 与 UI 文案中同步。
- 不把“估算结果”表述为 Anthropic 或 Claude 的官方结论。
- 新增依赖前检查静态输出和浏览器兼容性。

## 08. ROADMAP // 演进路线

- [x] 六类浏览器信号和中英双语页面
- [x] 静态输出、sitemap 与 PWA 资源
- [ ] 可导出的本地检测报告
- [ ] 更完整的浏览器兼容性测试矩阵

## 09. LICENSE // 许可证

仓库当前未附 LICENSE 文件，分发前请补充许可证并同步更新本节。本项目独立于 Anthropic/Claude。
