# The Attention Sanctuary

A minimalist digital intervention platform that acts as an "emergency brake" for the brain — helping users break out of doomscrolling and return to focused, deliberate attention.

## Pages

| Route | Description |
|---|---|
| `/` | Landing page with breathing motif and entry CTA |
| `/dashboard` | Gateway with three exercises: Calm My Body · Reset My Focus · Clear My Head |
| `/complete` | Conversion screen — account sign-up after completing an exercise |

## Tech

- [Astro](https://astro.build) — static site generator
- Tailwind CSS (CDN) — utility styling
- Lora + Inter — typography via Google Fonts
- Vanilla JS — all interactivity (no framework)

## Local development

**Prerequisites:** Node.js 18+

```bash
# 1. Install dependencies
npm install

# 2. Start the dev server (hot-reload on file save)
npm run dev
```

The site will be available at **http://localhost:4321**

## Build for production

```bash
# Outputs to dist/
npm run build

# Preview the production build locally
npm run preview
```

## Project structure

```
breatheapp/
├── src/
│   └── pages/
│       ├── index.astro       # / — landing
│       ├── dashboard.astro   # /dashboard — exercises
│       └── complete.astro    # /complete — conversion
├── screens/                  # original HTML prototypes (reference)
├── spec/PRD.md               # product requirements
├── astro.config.mjs
└── package.json
```
