# EpiBridge Presentations

> **View the live presentation: <https://kraemer-lab.github.io/EpiBridge-Presentations/>**

Slidev presentation deck for **EpiBridge**, an institutional research execution platform from the Kraemer Lab, University of Oxford.

## Quick start

```sh
pnpm install
pnpm dev
```

Opens `http://localhost:3030`. Edit `slides.md` to change the presentation.

## Commands

| Command | Description |
|---|---|
| `pnpm dev` | Start dev server with hot reload |
| `pnpm build` | Build static site to `dist/` |
| `pnpm export` | Export to PDF / PNG / PPTX |

## Deployment

| Platform | Config | Deploy trigger |
|---|---|---|
| GitHub Pages | `.github/workflows/deploy.yml` | Push to `main` |
| Netlify | `netlify.toml` | Netlify auto-deploy |
| Vercel | `vercel.json` | Vercel auto-deploy |

## Structure

```
slides.md        → presentation content (single file)
AGENTS.md        → context for AI coding assistants
netlify.toml     → Netlify deploy config
vercel.json      → Vercel deploy config
```

## Stack

- [Slidev](https://sli.dev/) v52 — Vue 3, Vite, UnoCSS
- Theme: `seriph`
- Diagrams: Mermaid
