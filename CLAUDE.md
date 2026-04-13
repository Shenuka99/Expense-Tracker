# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm install      # Install dependencies
npm run dev      # Start dev server at http://localhost:5173
npm run build    # Production build
npm run lint     # Run ESLint
npm run preview  # Preview production build
```

## Architecture

This is a React + Vite single-page app with no routing, no backend, and no state management library. All state lives in a single `useState`-heavy component: `src/App.jsx`.

**Known intentional issues (part of the course):**
- Bug: `amount` is stored as a string, so `reduce` concatenates instead of summing — totals are wrong
- Transaction #4 ("Freelance Work") is typed as `"expense"` but categorized as `"salary"` — data inconsistency
- No component decomposition — the entire UI is one monolithic component
- Styling is in `src/App.css` (component-scoped) and `src/index.css` (global resets/base)

**Data model** — each transaction:
```js
{ id, description, amount, type: "income"|"expense", category, date }
```

Categories are a hardcoded array: `["food", "housing", "utilities", "transport", "entertainment", "salary", "other"]`
