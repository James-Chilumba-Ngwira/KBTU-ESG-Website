# KBTU ESG Competence Center — Website

This repository showcases the website for the **KBTU ESG Competence Center**, which promotes Environmental, Social, and Governance (ESG) excellence in Central Asia through KBTU (Kazakh-British Technical University). It contains **two separate implementations** of the same site, built at different stages of the project:

| Folder | Stack | Purpose |
|---|---|---|
| [`KBTU-ESG-Website/`](KBTU-ESG-Website) | Plain HTML / CSS / vanilla JS | Lightweight, dependency-free static site. No build step — open directly or serve as static files. |
| [`esgkbtu-main/`](esgkbtu-main) | React + TypeScript + Vite + Tailwind + shadcn/ui | Modern component-based rebuild with routing, animations, and a full front-end toolchain. |

Both cover the same content: a home page introducing the ESG Competence Center and an ESG Principles page detailing the three ESG pillars, key policies, and initiatives.

---

## 1. `KBTU-ESG-Website/` — Static Site

A self-contained static website with no dependencies or build process.

**Structure:**
```
KBTU-ESG-Website/
├── index.html            # Home page (hero, about, services, offers, why-us)
├── esg-principles.html   # ESG Principles page (E/S/G pillars, policies, initiatives)
├── styles.css            # All styling (389 lines)
├── script.js             # Scroll-to-hash fix, mobile menu, language switch, scroll reveal
└── assets/               # Logo and images
```

**Key behaviors (`script.js`):**
- Re-corrects same-page anchor scrolling after web fonts finish loading (avoids layout shift from font swapping).
- Toggles the mobile hamburger menu.
- Handles a decorative language switch (UI only, no i18n backend).
- Reveals elements on scroll using `IntersectionObserver`.

**Fonts:** Fraunces (headings) and IBM Plex Sans/Mono (body), loaded from Google Fonts.

**To run:** just open `index.html` in a browser, or serve the folder with any static file server (e.g. `npx serve KBTU-ESG-Website`).

---

## 2. `esgkbtu-main/` — React/Vite Application

A modern rebuild using a component-driven front-end stack.

**Tech stack:**
- **React 18** + **TypeScript**
- **Vite** (build tool/dev server) with SWC
- **Tailwind CSS** + **shadcn/ui** (Radix UI primitives) for the design system
- **React Router** for client-side routing (`/`, `/esg-principles`, catch-all 404)
- **Framer Motion** for animations
- **React Query**, **React Hook Form + Zod**, **Recharts**, and other supporting libraries
- **Vitest** + **Testing Library** for tests
- **ESLint** for linting

**Structure:**
```
esgkbtu-main/
├── src/
│   ├── App.tsx                # Router setup and providers
│   ├── main.tsx                # App entry point
│   ├── pages/                  # Index, ESGPrinciples, NotFound
│   ├── components/             # Header, HeroSection, AboutSection, ServicesSection,
│   │                            #   SpecialOfferSection, WhyUsSection, Footer, NavLink
│   ├── components/ui/          # shadcn/ui component library
│   ├── hooks/                  # use-mobile, use-toast
│   ├── lib/utils.ts            # Shared utilities
│   └── assets/                 # Images used by the React build
├── public/                     # Static assets (favicon, robots.txt, placeholder)
├── dist/                       # Production build output (generated)
├── .github/workflows/deploy.yml  # GitHub Pages deployment workflow
├── netlify.toml                # Netlify build/redirect config
├── .vercel/                    # Vercel project metadata
├── vite.config.ts / vitest.config.ts / tailwind.config.ts / tsconfig*.json
└── package.json
```

**Available scripts** (run from within `esgkbtu-main/`):
```bash
npm install       # install dependencies
npm run dev       # start Vite dev server
npm run build     # production build → dist/
npm run build:dev # development-mode build
npm run preview   # preview the production build locally
npm run lint       # run ESLint
npm test          # run Vitest tests once
npm run test:watch # run Vitest in watch mode
npm run deploy     # build and publish dist/ to gh-pages
```

**Deployment:** This app is configured for multiple hosting targets:
- **GitHub Pages** via `.github/workflows/deploy.yml` (auto-deploys on push to `main`), with `App.tsx` using a `/KBTU-ESG-Website` basename in production.
- **Netlify** via `netlify.toml` (SPA redirect to `index.html`).
- **Vercel** via `.vercel/project.json`.

---

## License

MIT License — Copyright (c) 2026 James Chilumba Ngwira. See [LICENSE](LICENSE) for details.

## Notes

- The two site implementations are independent — changes to one do not affect the other. `esgkbtu-main/` also has its own nested `.git` repository, separate from this repo's top-level git history.
- If you're deciding which implementation to work from: use `KBTU-ESG-Website/` for quick edits with zero tooling, or `esgkbtu-main/` if you need componentization, routing, or a modern build pipeline.
