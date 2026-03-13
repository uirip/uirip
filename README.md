<p align="center">
  <img src=".github/assets/logo.svg" width="120" />
</p>

<h1 align="center">uirip</h1>

<p align="center">
  Reverse engineer any website from your terminal.<br/>
  Inspect components, compare pages, generate Next.js projects.
</p>

<p align="center">
  <a href="https://www.npmjs.com/package/uirip"><img src="https://img.shields.io/npm/v/uirip" alt="npm" /></a>
  <a href="https://www.npmjs.com/package/uirip"><img src="https://img.shields.io/npm/dm/uirip" alt="downloads" /></a>
  <a href="./LICENSE"><img src="https://img.shields.io/npm/l/uirip" alt="license" /></a>
</p>

<p align="center">
  <a href="https://ui.rip">Website</a> ·
  <a href="https://ui.rip/docs">Documentation</a> ·
  <a href="https://ui.rip/showcase">Showcase</a> ·
  <a href="https://ui.rip/free-inspector">Free Inspector</a>
</p>

---

## Install

```bash
npm install -g uirip
```

Or run without installing:

```bash
npx uirip inspect stripe.com
```

## Quick Start

### Inspect any website's components (free, no login)

```bash
uirip inspect stripe.com
# Components: nav, hero, pricing-table, testimonials, footer
# Tokens: 12 colors, 4 spacing values, 2 font families
# Framework: React (detected)
```

### Compare two pages pixel-by-pixel (free, no login)

```bash
uirip diff staging.example.com example.com
# Match: 99.2% | SSIM: 0.987 | Layout shifts: 0
```

### Reverse engineer a full site into a Next.js project

```bash
uirip login
uirip rip stripe.com
# ✔ Project written to ./stripe-com/
# Run: cd stripe-com && npm install && npm run dev
```

## What is uirip?

**uirip is a CLI that reverse engineers any website into clean,
deployable code.** Point it at a URL. It captures every page state,
detects component boundaries, extracts design tokens, and generates
a complete Next.js project — pixel-accurate to the original.

Unlike screenshot-to-code tools (v0, Bolt, Lovable) that generate UI
from text prompts, uirip works from **real production websites** — it
captures what actually exists, not what an AI imagines.

The CLI is open source. The intelligence runs on
**[ui.rip](https://ui.rip)**.

## How It Works

```
$ uirip rip <url>
     │
     ▼
┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐
│ Capture  │ →  │ Inspect  │ →  │ Analyze  │ →  │ Generate │ →  │ Verify   │
│ websnap  │    │ webprobe │    │ webast   │    │ web2next │    │ webdiff  │
└──────────┘    └──────────┘    └──────────┘    └──────────┘    └──────────┘
     │
     ▼
./stripe-com/   ← deployable Next.js project
```

| Stage | What It Does |
|-------|-------------|
| **Capture** | Multi-state SPA traversal, authenticated pages, full DOM snapshot |
| **Inspect** | Component boundary detection, design token extraction, layout graph |
| **Analyze** | Cross-page shared component detection, design system inference |
| **Generate** | HTML → JSX → deployable Next.js project |
| **Verify** | Pixel-diff comparison, structural similarity, layout shift detection |

Inspection and verification are also available as standalone packages:
[webprobe](https://github.com/uirip/webprobe) (npm) and
[webdiff](https://github.com/uirip/webdiff) (pip).

## Commands

| Command | What It Does | Auth |
|---------|-------------|:----:|
| `uirip inspect <url>` | Detect components, tokens, layout, framework | Free |
| `uirip diff <url1> <url2>` | Pixel-accurate visual comparison | Free |
| `uirip rip <url>` | Full pipeline → Next.js project | Login |
| `uirip login` | Authenticate with ui.rip | — |
| `uirip status` | Check plan and remaining quota | Login |

## Use Cases

- **Design system analysis** — Extract design tokens and component
  patterns from any production site
  ([try in browser](https://ui.rip/free-inspector))
- **Visual regression testing** — Catch pixel-level differences between
  deployments
- **Competitive UI research** — Inspect how top SaaS products structure
  their interfaces
- **Full reverse engineering** — Capture → analyze → generate a complete
  Next.js project
- **Learning** — Understand how Stripe, Linear, or Vercel build their
  frontends

## Comparison

| Feature | uirip | v0 | Bolt | Chrome DevTools | Puppeteer |
|---------|:-----:|:--:|:----:|:---------------:|:---------:|
| Works from existing sites | ✅ | ❌ | ❌ | ✅ | ✅ |
| Component detection | ✅ | ❌ | ❌ | ❌ | ❌ |
| Design token extraction | ✅ | ❌ | ❌ | Partial | ❌ |
| Code generation | ✅ | ✅ | ✅ | ❌ | ❌ |
| Pixel-diff verification | ✅ | ❌ | ❌ | ❌ | ❌ |
| SPA multi-state capture | ✅ | N/A | N/A | N/A | Partial |
| CLI interface | ✅ | ❌ | ❌ | N/A | ✅ |
| Open source | ✅ | ❌ | ❌ | ✅ | ✅ |

## FAQ

### What is UI reverse engineering?

UI reverse engineering is the process of analyzing a live website to
extract its component structure, design tokens, layout patterns, and
interaction states. Unlike "view source," it reconstructs the logical
architecture — identifying reusable components, shared layouts, and
design system patterns across multiple pages.

### How is uirip different from v0 or Bolt?

v0 and Bolt generate UI from text prompts — they create new interfaces
from imagination. uirip works from **existing production websites** —
it captures what's actually built. Use v0 when you have an idea. Use
uirip when you have a reference.

### Is the CLI free?

`uirip inspect` and `uirip diff` are completely free with no login.
`uirip rip` requires a free account and gives you 5 rips/month.
Upgrade at [ui.rip/pricing](https://ui.rip/pricing) for unlimited.

### What does the CLI send to your servers?

The CLI sends the target URL to the ui.rip API. All capture, analysis,
and generation happens server-side. Generated code streams back to your
terminal. We don't store generated projects. See our
[privacy policy](https://ui.rip/privacy).

### Can I self-host?

The CLI is open source (MIT). The backend pipeline is proprietary.
For inspection and diffing without any server dependency, use the
standalone packages:
[webprobe](https://github.com/uirip/webprobe) and
[webdiff](https://github.com/uirip/webdiff).

## Packages

The CLI wraps the full pipeline. These standalone packages run locally
with no server dependency:

| Package | Description | Install |
|---------|-------------|---------|
| [webprobe](https://github.com/uirip/webprobe) | Component detection + design tokens (browser-injectable) | `npm i webprobe` |
| [webdiff](https://github.com/uirip/webdiff) | Pixel-accurate visual regression testing | `pip install webdiff` |

## Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md). We welcome:
- Bug fixes, error handling improvements
- New output formats
- Better progress rendering
- Documentation and tutorials

We don't accept: features that move pipeline logic into the CLI.
The intelligence stays on the server — that's how we fund development.

## Links

- **[ui.rip](https://ui.rip)** — Full UI reverse engineering platform
- **[Free Inspector](https://ui.rip/free-inspector)** — Try webprobe
  in your browser, no install
- **[Showcase](https://ui.rip/showcase)** — See full pipeline results
- **[Documentation](https://ui.rip/docs)** — API reference and guides
- **[Blog](https://ui.rip/learn)** — Technical articles

## License

MIT — see [LICENSE](./LICENSE)

---

<p align="center">
  Built by <a href="https://ui.rip">ui.rip</a> — reverse engineer any UI
</p>
