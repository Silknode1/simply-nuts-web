# CLAUDE.md — Laser Engraving Designer Prototype

## Project Purpose
Self-contained React component for designing simple laser engravings that will be applied to the flat tops of bamboo barrels, wooden boxes, and aluminum gift tins for Simply Nuts & More.

## Stack
- React 18+ with TypeScript
- Fabric.js (preferred) or Konva for the canvas
- Framer Motion for all UI motion
- Tailwind CSS for chrome / controls
- Export: high-resolution transparent PNG (target 300+ DPI) and optional PDF via jsPDF or similar

## Core Requirements
- Support circle, square, and rectangle clipping masks that match product shapes.
- Logo upload (prefer transparent PNG). Place, scale, and rotate.
- Text tool: font, size, basic alignment. No background.
- Small library of simple holiday SVG elements (snowflake, Christmas tree, star, ornament, holly, gift box, candle). Each must support fill vs outline (stroke) modes.
- Per-element or global fill/outline toggle. Outlines should be clean and laser-friendly.
- All elements render with transparent backgrounds.
- Live preview of the design on the selected product shape.
- Export high-res transparent PNG. PDF as secondary option.
- Clean, responsive controls. Keyboard accessible where practical.

## Motion Guidelines
Use Framer Motion only for motion (no CSS transitions for scale, position, or opacity changes).

### Spring configurations
- Default: `{ type: "spring", damping: 25, stiffness: 250 }`
- Snappy: `{ type: "spring", damping: 15, stiffness: 400 }`
- Gentle: `{ type: "spring", damping: 30, stiffness: 200 }`

### Patterns
- Entrance: fade + slide up (y: 20 → 0) with default spring. Stagger children by ~60ms.
- Hover on buttons/cards: subtle scale (1.04) + lift (y: -2) with snappy spring.
- Tap/press: scale 0.97.
- Element selection feedback: soft scale or glow spring.
- Respect `prefers-reduced-motion`: show final state immediately or use simple opacity.

## Output Expectations
Return a reusable component (or small set of files) that can be dropped into a Next.js App Router project later. Keep dependencies minimal. Prioritize clean export quality for CorelDRAW handoff.

## Brand Notes (Simply Nuts & More)
Warm, family, slightly witty. Earthy palette (espresso browns, pine green, cream, copper/gold, deep red accents). Chippy the squirrel is the mascot but does not need to appear inside the designer canvas.
