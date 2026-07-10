# EpiBridge Presentations — AGENTS.md

## Project

Slidev presentation deck for EpiBridge, an institutional research execution platform from the Kraemer Lab, University of Oxford.

## Commands

```sh
npm run dev      # start dev server (opens http://localhost:3030)
npm run build    # build static site to dist/
npm run export   # export to PDF/PNG/PPTX
```

## Stack

- [Slidev](https://sli.dev/) v52 (Vue 3, Vite, UnoCSS)
- Theme: `seriph`
- Diagrams: Mermaid (native Slidev support)

## Structure

```
slides.md          → main presentation (single file, ~180 lines)
netlify.toml       → Netlify deploy config
vercel.json        → Vercel deploy config
AGENTS.md          → this file
```

## Style conventions

- **Audience:** epidemiology PIs and technical stakeholders — plain language, avoid jargon
- **Tone:** direct, concise, conceptual
- **Diagrams:** Mermaid `%%{init: {'theme': 'neutral'}}%%` blocks
- **Layouts:** CSS grid (`grid-cols-2 gap-8`) for two-column, `v-click` for incremental reveals
- **No boilerplate:** `Counter.vue`, `imported-slides.md`, `external.ts` were removed

## Key content notes

- EpiBridge is complementary to TREs, not a replacement
- Positions itself for smaller labs / single-machine deployments
- Core concepts: local development → sealed bundle → institutional execution → governed release
- Security: backend-authoritative, capability-based, immutable bundles, deterministic images, append-only audit

## Deployment

- Netlify: `npm run build` publishes `dist/` (Node 24, SPA fallback)
- Vercel: same build command, SPA rewrites
