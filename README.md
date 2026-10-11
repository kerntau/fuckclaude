# Fuck Claude — Are You a Claude “China User”?

English | 中文

A bilingual, privacy-first browser tool that estimates which environment signals could make Claude Code classify a session as a China user. The scan runs entirely in your browser: no telemetry, uploads, or network requests are used by the detector.

## What it checks

The page scores six browser-visible signals and shows the matched signals:

| Signal | Weight |
| --- | ---: |
| System timezone | 30 |
| Browser language | 24 |
| Installed Chinese fonts | 20 |
| Intl locale | 10 |
| UTC+8 offset | 8 |
| Emoji rendering hint | 8 |

Scores are combined into Low (0–30), Medium (31–60), and High (61–100) bands. This is an estimate based on public reverse-engineering reports, not an official Claude statement. A web page cannot inspect proxy hostnames or server-side settings.

## Tech stack

- Astro 7 with static output
- TypeScript detector module
- Built-in English (/) and Chinese (/zh/) pages
- @astrojs/sitemap
- pnpm

## Development

Requires Node.js 18+ and pnpm.

~~~bash
pnpm install
pnpm dev       # http://localhost:4321
pnpm build     # static output in dist/
pnpm preview
~~~

The optional asset generator is run with node scripts/gen-assets.mjs. Deploy the generated dist/ directory to a static host such as Cloudflare Pages, Vercel, Netlify, or GitHub Pages. Set site in astro.config.mjs and the origin in public/robots.txt before publishing so canonical URLs and the sitemap are correct.

## Project layout

~~~text
src/
├── config/signals.ts       # signal definitions and weights
├── config/sponsors.ts      # sponsor cards
├── i18n/ui.ts              # EN/ZH copy dictionary
├── scripts/detect.ts       # client-side scan and scoring
├── layouts/                # SEO metadata and global styles
├── components/             # detector, score ring, mascot and UI
└── pages/                  # English and Chinese routes
public/                     # mascot, sponsor assets and generated icons
scripts/gen-assets.mjs      # favicon/PWA/OG asset generation
~~~

## 中文说明

这是一个中英双语的本地浏览器检测工具，用于估算时区、语言、字体等环境信号是否呈现“中文环境”特征。检测结果仅供参考；时区是页面能读取且与 Claude Code 可能使用的操作系统时区相对应的信号，其他信号只是弱相关指纹。

~~~bash
pnpm install
pnpm dev
pnpm build
~~~

## Disclaimer

For reference and education only. The project is independent and is not affiliated with Anthropic or Claude.
