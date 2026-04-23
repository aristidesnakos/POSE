# SaaS Landing Page Hero Section

## Metadata
- **Category**: ui-components
- **Complexity**: Medium (200-800 LOC)
- **Output Type**: Single HTML file
- **Key Skills Tested**: Visual design, typography hierarchy, CTA placement, responsive layout, CSS animations, brand consistency
- **Dependencies**: None (single HTML file with embedded CSS + JS)

## Prompt

> Build a modern SaaS landing page hero section as a single self-contained HTML file with embedded CSS and JavaScript. No external libraries or frameworks.
>
> ### Design Requirements
>
> **Layout (top to bottom):**
> 1. **Navigation bar** — Logo on the left ("Flowly"), nav links in the center (Features, Pricing, Docs, Blog), and a "Get started free" CTA button on the right. Sticky on scroll.
> 2. **Hero content** — Centered, two-column layout:
>    - Left: Headline, subheadline, two CTA buttons, and social proof
>    - Right: Animated product UI mockup (browser chrome + dashboard screenshot using pure CSS/div elements — no images)
> 3. **Social proof strip** — Logos of "trusted by" companies rendered as styled text badges (e.g., Stripe, Notion, Linear, Vercel, Figma) in a muted row beneath the hero
>
> **Copy:**
> - Headline: "Ship faster with AI-powered workflows" (bold, large, gradient text)
> - Subheadline: "Flowly connects your tools, automates your busywork, and keeps your team in sync — so you can focus on what matters."
> - Primary CTA: "Start for free →" (filled button)
> - Secondary CTA: "Watch demo" (ghost button with play icon)
> - Social proof text: "Loved by 12,000+ teams worldwide ★★★★★"
>
> **Visual Style:**
> - Dark background: `#0a0a0f`
> - Accent gradient: `#7c3aed` → `#2563eb` (purple to blue)
> - Headline gradient text using the accent gradient
> - Card/surface color: `#12121a`
> - Border color: `rgba(255,255,255,0.08)`
> - Body text: `#94a3b8`
> - White text for headings
> - Font: system-ui stack (no external fonts)
>
> **Product mockup (right column):**
> - Browser chrome (three colored dots, URL bar) in a dark rounded card
> - Inside: A simplified dashboard UI made of divs:
>   - A sidebar with colored icon blocks and text stubs
>   - A main area with a fake bar chart (5 bars of varying heights using divs)
>   - Two stat cards at the top right showing "Tasks Done: 1,284" and "Time Saved: 47h"
> - The whole card should have a subtle purple glow (`box-shadow`)
> - Animate the card with a slow float up/down animation (3s ease-in-out infinite)
>
> **Navigation behavior:**
> - On scroll past 80px, the navbar adds a backdrop blur and border-bottom
> - "Get started free" button uses the accent gradient as background
>
> **Animations:**
> - Headline words fade in with a stagger (0.1s delay per word)
> - CTA buttons have a hover lift effect (`translateY(-2px)`)
> - Mockup card floats (keyframe animation)
>
> **Responsive:**
> - At < 768px, switch to single-column (content stacked above mockup)
> - Nav links collapse (just show logo + CTA button at mobile)

## Reference Materials

None — text-only prompt. All specifications are self-contained.

## Evaluation Checklist

- [ ] Opens in a browser without errors
- [ ] Navigation bar is present with logo, links, and CTA button
- [ ] Navbar becomes sticky/changes style on scroll
- [ ] Headline uses gradient text matching the accent colors
- [ ] Two-column layout with content left and product mockup right
- [ ] Product mockup is a CSS-only browser chrome with a dashboard inside
- [ ] Mockup card has a floating animation
- [ ] Both CTA buttons are present and visually distinct (filled vs ghost)
- [ ] Social proof strip with company name badges is visible
- [ ] Overall color scheme matches the dark theme specification
- [ ] Fade-in animation on the headline text
- [ ] Layout collapses to single column below 768px
- [ ] No external CSS libraries or JS frameworks used

## Notes for Evaluators

**This evaluation tests visual design and CSS animation skills.** The prompt specifies a dark SaaS-style hero — a very common real-world UI pattern. The key question is whether the output looks like something you'd ship.

**Common failure modes**:
- Model may reach for external libraries (Bootstrap, Tailwind CDN) — only acceptable if the prompt didn't explicitly forbid it, but the prompt says no external libraries
- Gradient text is frequently broken (the `background-clip: text` trick is easy to get wrong)
- Product mockup is often skipped or replaced with a placeholder image
- Responsive behavior is commonly omitted or broken
- Social proof strip may be forgotten

**What "close enough" means**: If the page looks like a real SaaS hero section — dark, modern, with a clear CTA and some kind of product visual — that's a strong pass. Pixel-perfect recreation of every spec isn't required, but the overall impression should be "this could ship."
