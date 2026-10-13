# CLAUDE.md — Simply Nuts & More Website

## Project Purpose
Modern, motion-rich website for Simply Nuts & More with two sides:
1. Nuts ecommerce (order by the pound + locations for fairs/shows).
2. Corporate holiday gifts with an integrated laser engraving designer.

## Stack
- Next.js (App Router) with TypeScript
- Tailwind CSS
- Framer Motion for all animations
- Supabase (database + storage for design files)
- Stripe (Checkout or Embedded Checkout)
- Deploy target: Vercel

## Architecture Conventions
- Server Components by default. Use `"use client"` only for interactivity (canvas, cart UI, motion).
- Prefer Server Actions and route handlers for mutations.
- Use Supabase SSR helpers (`@supabase/ssr`). Never expose service role key to the client.
- All Stripe calls happen server-side only. Verify webhooks.
- Store design file URLs (Supabase Storage) with order line items.
- Validate inputs with Zod at boundaries.
- Keep the first version simple: guest checkout only, no user accounts required.

## Motion Guidelines
Use Framer Motion only for motion (no CSS transitions for scale, position, or opacity).

### Spring configurations
- Default: `{ type: "spring", damping: 25, stiffness: 250 }`
- Snappy: `{ type: "spring", damping: 15, stiffness: 400 }`
- Gentle: `{ type: "spring", damping: 30, stiffness: 200 }`

### Patterns
- Page and section entrances: fade + slide up, stagger children.
- Product cards: subtle hover lift and scale.
- Buttons: hover scale 1.04, tap 0.97.
- Scroll-guided sections where they add clarity (not everywhere).
- Respect `prefers-reduced-motion`.

## Site Structure (target)
- Home: cinematic, scroll-guided feel with Chippy and product storytelling.
- Nuts: catalog by the pound, product detail, cart.
- Corporate Gifts: container selection (wooden boxes, bamboo, aluminum tins by size) → designer page/component → preview → cart.
- Locations: state fairs, arts & craft shows (simple list or map).
- Cart & Checkout: Stripe, handles both regular products and custom designs with attached PNG/PDF.

## Brand Direction
- Cleaner, more modern, and more interactive than the current simplynutsandmore.com.
- Warm family feel with witty edge. Earthy palette (espresso/walnut browns, pine green, cream, copper/gold, deep red logo accents).
- Typography: clean modern sans (Manrope or similar).
- Mascot: Chippy the Squirrel — use thoughtfully, not on every screen.
- Voice: warm, confident, solution-oriented. Avoid “cheap,” “bulk,” “factory.”

## Integration Notes
A separate laser engraving designer component (Fabric.js/Konva + Framer Motion) will be built first in Claude and then dropped into the corporate gifts product flow. On export, upload the high-res transparent PNG (or PDF) to Supabase Storage and attach the URL to the cart line item.

## Deferred for v1
- Returning customer accounts and pre-loaded designs.
- Full CSV recipient management.
- Real-time shipping rates and tax calculation (start with simple or manual).
- Admin production dashboard.
