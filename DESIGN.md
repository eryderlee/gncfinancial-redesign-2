# GNC Financial — Design System

## Brand Read

The GNC Financial logo is a confident, grounded wordmark. The uppercase "GNC" is set in a heavy, geometric sans-serif — broad strokes, tight tracking, no flourishes — projecting stability and directness. The single orange dot between the mark and the lowercase "gnc financial" text acts as both separator and punctuation: it says "full stop, we've got this." The lowercase treatment of the supporting text softens the authority of the caps, signalling approachability without sacrificing professionalism. There's generous negative space around every element — nothing is cramped or trying too hard. The overall impression is a firm that's been around, knows what it's doing, and doesn't need to shout about it. It reads as mid-2010s modern with timeless restraint — it would feel at home in a well-organised Bella Vista office park.

## Direction

**Primary: warm-advisory** / Fallback: modern-boutique

Warm-advisory fits because the logo's weight and earthiness already communicate trust and substance, while the lowercase text and orange accent add just enough warmth to avoid "big four" stiffness. The SME and tradie audience in the Hills District wants an accountant who feels local and human, not a corporate consultancy — warm-advisory delivers exactly that register.

## Type System

### Pairing: Fraunces (display) + Inter (text)

- **Display — Fraunces Variable** (Soft optical size, weights 400–700)
  Fraunces is an old-style soft serif with organic curves and just enough personality to feel approachable without being quirky. Its wedge-shaped serifs echo the solidity of the logo's uppercase "GNC" while introducing warmth that a geometric sans can't provide. Used for H1–H3 headings, pull-quotes, and the stat strip.

- **Text — Inter Variable** (weights 400–600)
  Inter is a workhorse — legible at every size, tuned for screens, unobtrusive. It lets the content do the talking. Used for body copy, navigation, form labels, captions, and UI elements.

### Scale (fluid, clamp-based)

| Token         | Min (mobile) | Max (desktop) | Weight  | Family   |
|---------------|-------------|---------------|---------|----------|
| `text-xs`     | 12px        | 12px          | 400     | Inter    |
| `text-sm`     | 13px        | 14px          | 400     | Inter    |
| `text-base`   | 15px        | 16px          | 400     | Inter    |
| `text-lg`     | 17px        | 18px          | 500     | Inter    |
| `text-xl`     | 20px        | 22px          | 500     | Inter    |
| `text-2xl`    | 24px        | 28px          | 500     | Fraunces |
| `text-3xl`    | 28px        | 36px          | 500     | Fraunces |
| `text-4xl`    | 34px        | 48px          | 600     | Fraunces |
| `text-5xl`    | 40px        | 60px          | 600     | Fraunces |

Line height: 1.5 for body, 1.15–1.25 for headings. Letter-spacing: -0.01em on headings, 0 on body.

## Colour System

### Ink (near-black — `#0E0E0E` base)

| Token      | Hex       | Use                            |
|------------|-----------|--------------------------------|
| `ink-50`   | `#F5F5F5` | Ink on dark backgrounds (inv.) |
| `ink-100`  | `#E5E5E5` | —                              |
| `ink-200`  | `#CCCCCC` | Disabled text                  |
| `ink-300`  | `#A3A3A3` | Placeholder text               |
| `ink-400`  | `#787878` | Muted captions                 |
| `ink-500`  | `#525252` | Secondary body text            |
| `ink-600`  | `#3D3D3D` | —                              |
| `ink-700`  | `#2E2E2E` | Body text (default)            |
| `ink-800`  | `#1A1A1A` | Headings                       |
| `ink-900`  | `#0E0E0E` | Logo-weight text               |
| `ink-950`  | `#050505` | Maximum contrast               |

### Accent (orange — `#E8801A` base)

| Token         | Hex       | Use                              |
|---------------|-----------|----------------------------------|
| `accent-50`   | `#FFF7ED` | Tinted background                |
| `accent-100`  | `#FFEDD5` | Hover bg on accent elements      |
| `accent-200`  | `#FED7AA` | —                                |
| `accent-300`  | `#FDBA74` | —                                |
| `accent-400`  | `#FB923C` | Hover state for CTA              |
| `accent-500`  | `#F97316` | —                                |
| `accent-600`  | `#E8801A` | **Primary accent** (logo orange) |
| `accent-700`  | `#C2610C` | Pressed/active state             |
| `accent-800`  | `#9A4E0F` | Dark mode accent (future)        |
| `accent-900`  | `#7C3F10` | —                                |
| `accent-950`  | `#431407` | Accent text on light bg          |

### Surface (warm off-white — `#FBF7F1` base)

| Token         | Hex       | Use                              |
|---------------|-----------|----------------------------------|
| `surface-50`  | `#FFFFFF` | Cards, elevated surfaces         |
| `surface-100` | `#FEFCF9` | Page background (alt sections)   |
| `surface-200` | `#FBF7F1` | **Primary background**           |
| `surface-300` | `#F5EDE1` | Dividers, subtle borders         |
| `surface-400` | `#EBE0D0` | Input borders                    |
| `surface-500` | `#D9CBBA` | —                                |
| `surface-600` | `#BBA998` | —                                |
| `surface-700` | `#9C8A79` | —                                |
| `surface-800` | `#7D6E5F` | —                                |
| `surface-900` | `#635849` | —                                |
| `surface-950` | `#4A4137` | Footer background                |

### Muted (warm grey — `#7A6E63` base)

| Token       | Hex       | Use                          |
|-------------|-----------|------------------------------|
| `muted-50`  | `#FAF8F6` | —                            |
| `muted-100` | `#F0EDE9` | —                            |
| `muted-200` | `#E0DAD4` | —                            |
| `muted-300` | `#C7BEB5` | Border default               |
| `muted-400` | `#A89D92` | Icon colour (secondary)      |
| `muted-500` | `#7A6E63` | **Base muted** — timestamps  |
| `muted-600` | `#655A50` | Caption text                 |
| `muted-700` | `#514841` | —                            |
| `muted-800` | `#3E3833` | —                            |
| `muted-900` | `#2D2925` | —                            |
| `muted-950` | `#1E1B18` | —                            |

### Accent Rationing Rule

> **One accent moment per viewport.** If a CTA button is orange, no other orange element should be visible at the same scroll position. Secondary CTAs use `ink-800` with an underline. Accent may also appear as the logo dot, a single rule line, or a hover state — never simultaneously.

## Layout System

- **Grid:** 12-column, `max-width: 1200px`, centered
- **Gutters:** 24px mobile / 32px desktop
- **Container padding:** 20px mobile / 40px desktop
- **Vertical rhythm:** 8px base unit
- **Section padding:** 96px top/bottom desktop / 56px mobile
- **Card gap:** 24px mobile / 32px desktop

### Breakpoints

| Name   | Width   |
|--------|---------|
| `sm`   | 640px   |
| `md`   | 768px   |
| `lg`   | 1024px  |
| `xl`   | 1280px  |

### Content widths

- Full-width sections: edge-to-edge background, content within `max-w-[1200px]`
- Prose/article: `max-w-[65ch]` centered
- Narrow (forms): `max-w-[560px]` centered

## Component Inventory

### 1. Header
- Logo top-left, nav links center/right, phone number far-right (desktop only)
- Mobile: hamburger menu, slide-in from right, full-height overlay
- Sticky on scroll with subtle `surface-50` background + shadow
- Active page indicated by accent underline

### 2. Sticky CTA
- Mobile-only fixed bottom bar: "Book a free consult" button, full-width
- Disappears when footer is visible (Intersection Observer)
- `accent-600` background, white text

### 3. Hero
- Full-width `surface-200` background
- H1 (Fraunces, `text-5xl`), one-line subtitle (Inter, `text-lg`, `ink-500`)
- Primary CTA button + secondary text link
- No hero image — rely on typography and space
- Optional: subtle accent dot decorative element echoing the logo

### 4. Service-Group Card
- White card (`surface-50`) with `surface-300` border
- Icon (Lucide, `muted-400`, 24px) — optional, only if adding clarity
- H3 title (Fraunces), 2-line description (Inter), text link "Learn more →"
- Hover: slight lift (`translateY(-2px)`) + border transitions to `accent-600`
- 5 cards in a responsive grid: 1 col mobile, 2 col tablet, 3 col desktop (last row centered)

### 5. Stat Strip
- Full-width `ink-900` background, white text
- 4 stats in a row: large number/label (Fraunces) + descriptor (Inter, `ink-200`)
- Single row on desktop, 2×2 grid on mobile

### 6. Testimonial Pull-Quote
- Large opening quotation mark in `accent-600` (decorative, Fraunces)
- Quote text in `text-xl` Inter italic
- Attribution: first name + suburb, `muted-500`, `text-sm`
- 3 quotes in a horizontal scroll on mobile, 3-column grid on desktop

### 7. Insight Card
- Vertical card: category pill (accent-50 bg, accent-950 text), date (muted), H3 title, 60-word excerpt, "Read more →" link
- Grid: 1 col mobile, 3 col desktop

### 8. FAQ Accordion
- Clean expand/collapse with Lucide `ChevronDown` icon
- Only one open at a time
- Question in `text-lg` Inter 500, answer in `text-base` Inter 400
- Subtle `surface-300` divider between items
- No animation beyond 200ms height transition

### 9. Footer
- `surface-950` background, `surface-200` text
- 3-column layout: (1) logo + tagline, (2) nav links + legal links, (3) contact info + social icons
- Google Map embed (small, rounded corners)
- IPA badge (placeholder until verified)
- © 2026 GNC Financial

### 10. Contact Form
- Web3Forms integration
- Fields: Name, Email, Phone, Message (textarea)
- Labels above fields, `surface-50` input backgrounds, `surface-400` borders
- Focus: `accent-600` border, accent ring
- Submit button: `accent-600` bg, white text
- Inline success (green) / error (red) messages below form
- Honeypot field for spam

## Motion

- **Duration:** 200ms default, 300ms for layout shifts (accordion, mobile menu)
- **Easing:** `ease-out` for entrances, `ease-in-out` for state changes
- **Scroll:** Elements fade-in with `translateY(16px)` on first viewport entry (optional — `prefers-reduced-motion` respected)
- **Hover:** 150ms color/border transitions
- **No:** parallax, auto-rotating carousels, bouncing elements, loading spinners beyond a simple pulse, video backgrounds

## Anti-Patterns — Explicitly Banned

1. **No stock photos** of generic handshakes, city skylines, or smiling diverse teams
2. **No glassmorphism**, gradient blobs, or neon effects
3. **No two competing accent colours** — orange is the only accent
4. **No Bootstrap-default cards/shadows** — our shadows are subtle and warm-toned if used at all
5. **No filler copy** like "we are a team of passionate experts" or "your success is our passion"
6. **No empty service-detail sub-pages** with duplicate body text — Services is one page with anchors
7. **No "trusted by" logo wall** unless we have real partner logos with written permission
8. **No carousels**, auto-playing video, or chat widget pop-ups
9. **No purple, teal, or corporate-blue** — accent is orange-only
10. **No suburb-doorway pages** for SEO — one site, real content
11. **No "bloody effective"** or overly casual copy — warm and plain-English, but professional
12. **No duplicate pages** (e.g., separate "Book Now" page that mirrors Contact)
13. **No AI-generated headshots** or team photos
14. **No auto-playing anything** — user initiates all interactions
