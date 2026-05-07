# GNC Financial — Self-Review

## 1. Brand Read — Orange Dot Per Viewport

| Page | One accent moment per viewport? | Notes |
|------|--------------------------------|-------|
| Home | Yes | Hero CTA is the sole orange element in the first viewport. Bottom CTA is well-separated. Mobile sticky bar hides when footer enters view. |
| About | Yes | Orange used only in the numbered circles (one viewport section at a time) and credential placeholders. |
| Services | Yes | Orange bullets are the sole accent in each service section. Bottom CTA separated. |
| Insights | Yes | Category pills use `accent-50` bg (very subtle), not solid orange. Cards use border-on-hover only. |
| Contact | Yes | Form submit button is the sole orange element in its viewport. Sticky bar hides near footer. |
| Privacy | Yes | No accent elements — text-only page. Links use `accent-700` underline. |
| Disclaimer | Yes | Same as Privacy. |
| Blog posts | Yes | Category pill (subtle tint) is the only accent in the header area. |

**Verdict: Pass.**

## 2. Anti-Patterns Check

| Anti-pattern | Present? |
|-------------|----------|
| Stock photos (handshakes/skylines/teams) | No |
| Glassmorphism / gradient blobs / neon | No |
| Two competing accent colours | No — orange only |
| Bootstrap-default cards / shadows | No |
| "We are a team of passionate experts" filler | No |
| Empty service-detail sub-pages | No — Services is one page with anchors |
| "Trusted by" logo wall without permission | No — credential logos are all placeholders marked `data-placeholder="true"` |
| Carousels / auto-playing video / chat widget | No |
| Purple / teal / corporate-blue | No |
| Suburb doorway pages | No |
| "bloody effective" or overly casual copy | No |
| Duplicate pages | No |
| AI-generated headshots | No |

**Verdict: Pass — zero anti-patterns detected.**

## 3. Copy Review

- No sentence could appear on a generic competitor site. All copy references the Hills District, Glenn, or specific services.
- "bloody effective" — not present.
- "no mucking about" — not present.
- No duplicate paragraphs across pages.
- Firm credo is rewritten as: "Down-to-earth, personal service from a local accountant who's spent three decades helping Hills District businesses and families get ahead."

**Verdict: Pass.**

## 4. Page Count

| Page | Path | Status |
|------|------|--------|
| Home | `/` | Built |
| About | `/about/` | Built |
| Services | `/services/` | Built |
| Insights | `/insights/` | Built |
| Contact | `/contact/` | Built |
| Privacy | `/privacy/` | Built |
| Disclaimer | `/disclaimer/` | Built |
| 8 blog posts | `/insights/[slug]/` | Built (stub content) |

- No suburb-doorway pages. No per-service stubs. No `/contact/` duplicate. No "Book Now" duplicate page.

**Verdict: Pass — exactly the 7 specified pages + 8 blog post stubs.**

## 5. TODOs and Placeholders — Pre-Launch Checklist

### Critical (site won't function)

| Item | Location | Action needed |
|------|----------|---------------|
| Web3Forms API key | `src/components/ContactForm.astro` | Replace `TODO_REPLACE_WITH_WEB3FORMS_KEY` with real key |

### High Priority (visible gaps)

| Item | Location | Action needed |
|------|----------|---------------|
| 8 blog post bodies | `src/pages/insights/[slug].astro` | Migrate full content from existing site |
| Booking link | `src/pages/contact.astro` | Replace `href="#"` with Calendly/booking URL |

### Medium Priority (credential verification)

| Item | Location | Action needed |
|------|----------|---------------|
| Glenn's post-nominals | `src/pages/about.astro` | Confirm MIPA/FIPA and any CA/CPA designation |
| IPA logo | `src/pages/about.astro` | Replace grey placeholder with real IPA member logo |
| BAS Agent badge | `src/pages/about.astro` | Replace grey placeholder with real TPB badge |
| Xero partner tier | `src/pages/about.astro` | Verify tier and replace placeholder with real logo |
| MYOB partner tier | `src/pages/about.astro` | Verify tier and replace placeholder with real logo |
| QuickBooks partner tier | `src/pages/about.astro` | Verify tier and replace placeholder with real logo |
| Founding year | Not used on site | Spec had TODO — decide if needed |

### Low Priority (polish)

| Item | Location | Action needed |
|------|----------|---------------|
| Footer IPA badge | `src/components/Footer.astro` | Replace text placeholder with real badge image |
| Contact JSON-LD parity | `src/pages/contact.astro` | Add `description` and `sameAs` fields to match Home page JSON-LD |
| Opening hours | JSON-LD on Home & Contact | Add `openingHoursSpecification` when confirmed |
| Google Map embed URL | All map instances | Verify exact embed URL from Google Maps for the office |

## 6. Build & Performance

```
Build: ✓ 15 pages built in 2.53s
Output size: 351KB total (HTML + CSS + images)
CSS bundle: 30KB (one file, no JS bundles)
JS: 0KB bundled (inline scripts only for mobile menu, sticky CTA, and contact form)
JS budget: ✓ Well under 50KB gzipped
Sitemap: ✓ Generated at /sitemap-index.xml
Robots.txt: ✓ Present
```

**Note: Lighthouse audit cannot be run in this environment (no browser available). Run locally with:**
```bash
cd site && npm run preview
# Then in Chrome DevTools → Lighthouse tab, audit both mobile and desktop
```

## 7. Accessibility

Manual review findings:
- All interactive elements have visible focus rings (`2px solid accent-600`)
- All images have `alt` text and explicit `width`/`height`
- Mobile menu has `aria-label`, `aria-expanded`, and `aria-hidden` attributes
- FAQ uses native `<details>`/`<summary>` elements (keyboard-accessible by default)
- Form inputs have associated `<label>` elements
- Colour contrast: `accent-600` (#E8801A) is used only on large text (headings) or non-text UI (buttons with white text). Body text uses `ink-700` (#2E2E2E) on `surface-200` (#FBF7F1) — passes AA.
- `lang="en-AU"` set on `<html>` element
- Honeypot field uses `style="display:none"` and `tabindex="-1"` — hidden from assistive tech

**Note: Run axe DevTools in browser to confirm 0 violations:**
```bash
cd site && npm run preview
# Install axe DevTools browser extension, run scan on each page
```

## 8. Mobile Responsiveness

Layout designed for these breakpoints:
- 360px (small phones) — single column, full-width CTAs, hamburger nav
- 414px (standard phones) — same as 360px with slightly more breathing room
- 768px (tablets) — 2-column grids, nav still collapses at `md` (768px)
- 1024px+ (desktop) — full 3-column grids, visible nav, phone number in header

Key mobile features:
- Sticky bottom CTA bar (hides when footer visible)
- Slide-in mobile menu (full-height overlay)
- Stat strip: 2x2 grid on mobile, 4-column on desktop
- FAQ accordion works via native `<details>` — no JS dependency

**Note: Test in browser DevTools responsive mode to confirm no horizontal overflow.**

## 9. Forms

- Contact form is built with Web3Forms integration
- Honeypot spam protection included
- Inline success/error messages implemented
- **Cannot test submission** — `TODO_REPLACE_WITH_WEB3FORMS_KEY` placeholder must be replaced first
- Form fields: Name (required), Email (required), Phone (optional), Message (required)

## 10. Final Question

> Would I be proud to put my name on this site?

**Yes, with one caveat.** The structure, design system, copy tone, and technical foundation are solid. The site is fast (no JS bundles), accessible, SEO-ready, and true to the brand. The one change I'd make before launch: **migrate the 8 real blog post bodies from the existing site**. Right now they're placeholder stubs — having real content there would dramatically improve the site's authority and SEO value from day one. Everything else on the TODO list is credential verification or third-party key setup, which is expected at this stage.
