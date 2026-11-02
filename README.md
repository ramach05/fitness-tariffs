# Fitness Club Tariffs

🇬🇧 **English** | [🇷🇺 Русский](README.ru.md)

[![CI](https://github.com/ramach05/fitness-tariffs/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/ramach05/fitness-tariffs/actions/workflows/ci.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

A gym membership landing page: a live promo countdown, tariff cards fetched
from an API with the recommended plan pinned first, terms consent and a
purchase flow. Next.js 15 (App Router), React 19, Tailwind CSS.

## Screens

| Desktop | Mobile (timer warning, ≤ 30 s) | Mobile (timer expired) |
| --- | --- | --- |
| <img src="screenshots/main-page-desktop.png" alt="Desktop layout" width="360" /> | <img src="screenshots/main-page-mobile-timer-alert.png" alt="Mobile, timer in warning state" width="220" /> | <img src="screenshots/main-page-mobile-timer-done.png" alt="Mobile, timer expired" width="220" /> |

## Highlights

- **Live countdown** — updates every second; switches to a red blinking state
  at 30 s; on expiry discounts hide and cards show full prices only.
- **Recommended plan first** — the `is_best` tariff renders as a hero card,
  the rest in a responsive grid (1 / 2 / 3 columns).
- **Discount badges** — percent off computed from `price` vs `full_price`,
  shown with a struck-through original.
- **Purchase gate** — buy is blocked until the recurring-payment terms
  checkbox is ticked; the error clears on consent.
- **Data from a real endpoint** — tariffs fetched at runtime, with loading
  and error states.

## Features

- Countdown header with promo state.
- Clickable tariff cards; the selected one is highlighted; any plan can be
  picked before purchase.
- Terms-consent checkbox with validation.
- "Choose 3+ months" info block and a 30-day money-back guarantee block.
- Fully responsive (mobile-first), fonts via `next/font`.

## Data

Tariffs are loaded from `https://t-core.fit-hub.pro/Test/GetTariffs` — an
array of `{ id, period, price, full_price, is_best, text }`.

## Structure

```
├── app/
│   ├── layout.tsx    # Root layout, fonts, metadata
│   ├── page.tsx      # Home page (timer, tariffs, purchase form)
│   └── globals.css   # Global styles and utilities
├── components/
│   ├── Header.tsx          # Header with promo timer
│   ├── TariffList.tsx      # Hero card + grid
│   ├── TariffCard.tsx      # Single tariff card
│   ├── CheckboxBlock.tsx   # Terms consent
│   └── GuaranteeBlock.tsx  # Money-back block
├── lib/
│   ├── types.ts   # Tariff type
│   └── api.ts     # fetchTariffs()
└── utils/
    └── price.ts   # formatPrice(), getDiscountPercent()
```

## Implementation notes

- Components are wrapped in `React.memo`; callbacks stabilized with
  `useCallback`, the tariff list with `useMemo`.
- Arrow-function components and utilities; types and effects documented with
  JSDoc.
- Responsive layout: mobile cards are two columns (price | description);
  desktop is hero left, content right.

## Quick start

Requires Node.js 18+.

```bash
npm install
npm run dev   # http://localhost:3000
```

| Script | Description |
| --- | --- |
| `npm run dev` | Dev server with hot reload |
| `npm run build` | Production build |
| `npm start` | Serve the production build |
| `npm run typecheck` | TypeScript check |

Requires Node.js 18+.

## License

MIT
