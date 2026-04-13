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

This is a React + Vite single-page app with no routing, no backend, and no state management library.

**Component tree:**
```
App                      — holds transactions state and handleAdd callback
├── Summary              — receives transactions, computes totalIncome/totalExpenses/balance internally
├── TransactionForm      — owns its own form state; calls onAdd(transaction) on submit
└── TransactionList      — receives transactions, owns its own filter state (filterType, filterCategory)
```

**State ownership:**
- `transactions` array lives in `App` and is passed down as props
- Form fields (`description`, `amount`, `type`, `category`) are local to `TransactionForm`
- Filter state (`filterType`, `filterCategory`) is local to `TransactionList`

**Data model** — each transaction:
```js
{ id, description, amount, type: "income"|"expense", category, date }
```

`amount` is a number. `categories` is a hardcoded array duplicated in `TransactionForm` and `TransactionList`: `["food", "housing", "utilities", "transport", "entertainment", "salary", "other"]`

Styling is in `src/App.css` (component-scoped) and `src/index.css` (global resets/base).
