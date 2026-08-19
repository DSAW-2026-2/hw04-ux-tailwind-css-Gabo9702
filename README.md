# Name
Carlos Gabriel Rodríguez Ornelas
# Link page
https://dsaw-2026-2.github.io/hw04-ux-tailwind-css-Gabo9702/

# HW04 — UX + Tailwind CSS

**Week 4 · DSAW · Universidad de La Sabana**

## Objective

Create complete wireframes for your project in Figma and rebuild the landing page with Tailwind CSS, including a working dark mode toggle.

## Deliverables

### `index.html`

Rebuild your landing page using **Tailwind CSS** (via CDN or Vite):
- Use utility classes for **all** styling — no separate custom CSS file
- Responsive using Tailwind's prefixes: `sm:`, `md:`, `lg:` — no manual media queries
- Implement a **working dark mode toggle** using Tailwind's `dark:` variant:
  - There must be a visible button that switches between light and dark mode
  - The switch must affect background colors, text, and at least one component

### `figma-link.txt`

URL to your Figma file containing wireframes for **all main screens** of the project:
- At least 3 distinct screens
- Each screen must show at least 3 states: empty, with data, and error/validation

## Layer 2

The dark mode toggle must persist across page reloads using `localStorage`.

## AI Log (`AI-LOG.md`)

- Did you use AI to generate Tailwind classes? Did you also use it for the wireframes?
- What did you learn about Tailwind that you wouldn't have learned if AI had done everything?

## Deployment

GitHub Pages. If you use Vite, configure the `base` option in `vite.config.js`.

## Autograding

The pipeline will check:
- ✅ `index.html` and `figma-link.txt` are present
- ✅ HTMLHint passes with no errors
- ✅ GitHub Pages responds with HTTP 200
- ✅ Tailwind used correctly, dark mode works, wireframes complete (reviewed by Claude)

> **Submission rule:** If it is not deployed and public, it cannot be graded.
