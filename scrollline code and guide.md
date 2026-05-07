Found it — it's the curved red SVG line in `src/components/ui/ScrollLine.tsx` that draws itself in via GSAP ScrollTrigger as you scroll, and bends to land on the Contact CTA button. Below is a self-contained handoff packet for your other agent.

---

# Handoff: Scroll-Drawn Line Component

## What it does
A curved SVG path is rendered behind a section of the page. As the user scrolls through that section, GSAP ScrollTrigger animates the `stroke-dashoffset` so the line "draws itself" from top to bottom. The path is shaped with two cubic bezier sweeps, and its end-point is locked onto the horizontal+vertical position of a target element (a CTA button) so the line "lands" on it. It also fires `cta-line-reached` / `cta-line-left` custom events when the tip of the line hits the target.

## Stack assumptions
- Next.js (App Router) with React 19 + TypeScript
- Tailwind (v4) for the wrapper utility classes — easily replaceable with plain CSS
- **GSAP 3** with the **ScrollTrigger** plugin

If your other site is plain React/Vite/CRA, the component works identically — only the `'use client'` directive is Next-specific (you can delete it).

## Install dependency
```bash
npm install gsap
```
(Project uses `gsap@^3.15.0`. ScrollTrigger ships in the main `gsap` package — no separate install.)

## The component — `ScrollLine.tsx`

Drop this anywhere in your components folder. It expects a target element with `id="contact-cta"` somewhere later on the page (rename the id if you want — see "Customizing" below).

```tsx
'use client';

import { useEffect, useRef } from 'react';
import { gsap } from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger);

// Two wide sweeps ending precisely at the target element's centre.
// endX lets the path land at the target's horizontal position rather than
// always at viewport centre.
function buildPath(cx: number, endY: number, amp: number, endX: number): string {
  const cp1x = cx - amp * 0.26;
  const cp2x = cx - amp;
  const mid   = endY * 0.50;
  const peak2 = endY * 0.75;
  const scp1x = cx + amp * 0.5;
  return (
    `M ${cx} 0 ` +
    `C ${cp1x} ${endY * 0.13}, ${cp2x} ${endY * 0.30}, ${cx} ${mid} ` +
    `S ${scp1x} ${peak2}, ${endX} ${endY}`
  );
}

export default function ScrollLine() {
  const wrapperRef = useRef<HTMLDivElement>(null);
  const svgRef     = useRef<SVGSVGElement>(null);
  const pathRef    = useRef<SVGPathElement>(null);

  useEffect(() => {
    const wrapper = wrapperRef.current;
    const svg     = svgRef.current;
    const path    = pathRef.current;
    if (!wrapper || !svg || !path) return;

    let st: ScrollTrigger | null = null;

    const setup = () => {
      st?.kill();

      const cta = document.getElementById('contact-cta');
      if (!cta) return;

      const wRect = wrapper.getBoundingClientRect();
      const cRect = cta.getBoundingClientRect();
      const svgW  = wRect.width;

      const endY =
        (cRect.top + window.scrollY) -
        (wRect.top + window.scrollY);

      svg.setAttribute('width', String(svgW));
      svg.style.height = `${endY}px`;

      const amp  = svgW * 0.40;
      const cx   = svgW * 0.5;
      const endX = cRect.left + cRect.width / 2 - wRect.left;

      path.setAttribute('d', buildPath(cx, endY, amp, endX));

      const totalLen = path.getTotalLength();
      path.style.strokeDasharray  = String(totalLen);
      path.style.strokeDashoffset = String(totalLen);

      let ctaReached = false;

      st = ScrollTrigger.create({
        trigger: wrapper,
        start:   'top 80%',
        end:     `top+=${endY} 80%`,
        scrub:   1.2,
        onUpdate(self) {
          const offset = totalLen * (1 - self.progress);
          path.style.strokeDashoffset = String(offset);

          const drawnLen = Math.max(0, totalLen - offset - 1);
          const tipSVG  = path.getPointAtLength(drawnLen);
          const svgRect = svg.getBoundingClientRect();
          const ctaRect = cta.getBoundingClientRect();
          const tipY    = svgRect.top + tipSVG.y;
          const nearCta = tipY >= ctaRect.top - 4;

          if (!ctaReached && nearCta) {
            ctaReached = true;
            document.dispatchEvent(new CustomEvent('cta-line-reached'));
          } else if (ctaReached && !nearCta) {
            ctaReached = false;
            document.dispatchEvent(new CustomEvent('cta-line-left'));
          }
        },
      });
    };

    const raf = requestAnimationFrame(setup);
    window.addEventListener('resize', setup);
    return () => {
      cancelAnimationFrame(raf);
      window.removeEventListener('resize', setup);
      st?.kill();
    };
  }, []);

  return (
    <div
      ref={wrapperRef}
      className="absolute inset-0 pointer-events-none opacity-50 md:opacity-100"
      style={{ zIndex: 1 }}
      aria-hidden="true"
    >
      <svg
        ref={svgRef}
        style={{ position: 'absolute', top: 0, left: 0, overflow: 'visible' }}
        fill="none"
      >
        <path
          ref={pathRef}
          stroke="rgba(230,57,70,0.45)"
          strokeWidth="1.5"
          strokeLinecap="round"
          fill="none"
        />
      </svg>
    </div>
  );
}
```

## How to mount it

The component absolute-positions itself, so its parent **must be `position: relative`** and contain all the sections you want the line to pass through. The target button must live inside that same container.

```tsx
<div className="relative">
  <ScrollLine />
  <Projects />
  <Experience />
  <Skills />
  <Contact /> {/* contains <button id="contact-cta">…</button> */}
</div>
```

If you're not using Tailwind, the parent just needs:
```css
.scroll-line-parent { position: relative; }
```

## Customizing for the new site

| Want to change | Where |
|---|---|
| Target element | Replace `'contact-cta'` (line: `getElementById('contact-cta')`) with your own id |
| Line color | `stroke="rgba(230,57,70,0.45)"` on the `<path>` |
| Line thickness | `strokeWidth="1.5"` |
| Curve width | `const amp = svgW * 0.40` — fraction of container width the curves swing out |
| When drawing starts | `start: 'top 80%'` (when wrapper top hits 80% of viewport) |
| Scroll smoothing | `scrub: 1.2` — higher = smoother lag, `true` = 1:1 with scroll |
| Mobile fade | `opacity-50 md:opacity-100` Tailwind classes on the wrapper |

## Optional — the custom events
If you don't need the "line reached the button" hook (e.g. for a shockwave / glow on the CTA), you can delete the `ctaReached` block and the `dispatchEvent` calls. To consume them elsewhere:
```ts
document.addEventListener('cta-line-reached', () => { /* play effect */ });
document.addEventListener('cta-line-left',     () => { /* reset */ });
```

## Gotchas to flag to the other agent
1. **Parent must have `position: relative`** and span the full vertical range you want the line drawn over.
2. **Target element must exist** at first paint — if it's lazy-rendered, call `ScrollTrigger.refresh()` after it mounts, or re-run `setup`.
3. **Tailwind v4 inline-theme** — the original project uses Tailwind v4 with `@theme` tokens in `globals.css`, no `tailwind.config.js`. If your target site uses Tailwind v3, the wrapper classes (`absolute inset-0 pointer-events-none opacity-50 md:opacity-100`) still work as-is.
4. **Smooth-scroll libraries** — the source site uses Lenis. ScrollTrigger works fine with Lenis or native scroll; nothing in this component needs adjusting for either.
5. **Next.js** — the `'use client'` directive is required in App Router; remove it for Vite/CRA/Remix.

That's everything the other agent needs.