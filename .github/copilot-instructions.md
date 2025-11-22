<!-- .github/copilot-instructions.md: guidance for AI coding agents working on this repo -->
# Copilot / AI agent instructions — Next.js Developer Portfolio Starter

Quick summary
- This is a small Next.js (pages-router) portfolio starter. Key code lives under `src/pages` (React pages and API routes), styles live in `src/styles` (global CSS + CSS modules), and static assets are in `public/` and `website images/`.

Fast commands
- Install: `npm install`
- Dev server: `npm run dev` (runs `next dev`)
- Build: `npm run build` then `npm run start` for production
- Lint: `npm run lint`

Big picture / architecture
- Router: Uses the Next.js pages router. Edit page components in `src/pages/*.js` (e.g., `src/pages/index.js`).
- Static assets: `public/` holds images and `public/All-Texts/*.txt` (site copy snippets). These are static files served at `/<path>` and commonly referenced by pages.
- Styling: Global CSS in `src/styles/globals.css`. Component/page styles use CSS Modules (example: `src/styles/Home.module.css`) — not Tailwind in the actual codebase.
- API: Serverless API routes live in `src/pages/api/*.js` (example: `src/pages/api/hello.js` returns JSON). Use these for small backend endpoints.

Project-specific notes (do not assume common README claims)
- The repository README mentions Tailwind, but the codebase uses plain CSS + CSS modules and `globals.css`. Do not add Tailwind or refactor to Tailwind unless the user asks.
- `framer-motion` is listed as a dependency; animation code may be present in forks or intended features, but current pages are a default Next.js template. Import `framer-motion` when adding animations.
- Next.js version is v14 (see `package.json`) but the project still uses `src/pages` (pages router). Avoid migrating to the `app/` router unless instructed.

Common editing tasks — concrete file targets
- Edit homepage copy: `src/pages/index.js` and `src/styles/Home.module.css` or `public/All-Texts/pages.txt` (update the static copy file if content should be reused across builds).
- Add a new page: create `src/pages/<name>.js` and a corresponding CSS module in `src/styles` if needed.
- Add an API endpoint: create `src/pages/api/<endpoint>.js`. Mirror the `handler(req,res)` pattern from `src/pages/api/hello.js`.
- Add an image asset: put the file under `public/images/` or `website images/` and reference with `next/image` (`/images/<file>`).

Debugging & developer workflow
- Local dev: `npm run dev` shows React/Next overlay errors in browser; use server logs for runtime API errors.
- API test: call `http://localhost:3000/api/hello` to check route responses.
- Production test: `npm run build` then `npm run start` — watch for build errors related to imports or image sizes.

Patterns and conventions to respect
- Keep pages under `src/pages` (file-based routing). Avoid changing directory layout.
- Use CSS Modules for page-level styles (import as `styles from '@/styles/Name.module.css'`). Global tokens and variables belong in `src/styles/globals.css`.
- Static copy is sometimes stored in plaintext under `public/All-Texts/*.txt` — search and update those files when editing site copy.
- Prefer `next/image` for images already used in `src/pages/index.js` (it requires images to be in `public/` or configured domains).

External deps & integration points
- `next`, `react`, `react-dom` — core framework. Follow Next.js v14 docs for behavior.
- `framer-motion` — used for animations if added; import per component.
- No server/database integrations present — only serverless API routes under `src/pages/api`.

Examples (copy/paste targets)
- Simple API route (pattern exists in `src/pages/api/hello.js`):
```
export default function handler(req, res) {
  res.status(200).json({ name: 'John Doe' })
}
```
- Dev run:
```
npm install
npm run dev
```

When in doubt
- Search code for the string you plan to change (e.g., a header text) — the repo often stores copy in `public/All-Texts/*.txt`.
- Do not introduce major structural changes (router migration, Tailwind) without an explicit request.

If you edit this file
- Keep it short and concrete. Add references to new conventions only when they appear in the code.

Feedback
- If anything above is unclear or a follow-up is needed (specific pages, tests, CI, or intended Tailwind migration), tell me which area to expand.
