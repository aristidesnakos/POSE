# SaaS Pricing Table

## Metadata
- **Category**: ui-components
- **Complexity**: Medium (200-800 LOC)
- **Output Type**: Single HTML file
- **Key Skills Tested**: UI layout, interactive toggle, conditional rendering, visual hierarchy, responsive design
- **Dependencies**: None (single HTML file with embedded CSS + JS)

## Prompt

> Build a SaaS pricing table as a single self-contained HTML file with embedded CSS and JavaScript. No external libraries or frameworks.
>
> ### Product Context
>
> The product is "Flowly" — a project management and automation tool. Three pricing tiers: Starter, Pro, and Enterprise.
>
> ### Layout Requirements
>
> **Page structure:**
> 1. **Header** — Centered section title "Simple, transparent pricing" with subtitle "No hidden fees. Cancel anytime."
> 2. **Billing toggle** — Pill-style toggle switch between "Monthly" and "Annually" (with "Save 20%" badge next to Annual)
> 3. **Pricing cards** — Three cards side by side (Starter, Pro, Enterprise). The "Pro" card is highlighted as the recommended tier.
> 4. **FAQ accordion** — Below the cards, a simple accordion with 4 common pricing questions
>
> **Pricing tiers:**
>
> | | Starter | Pro | Enterprise |
> |---|---|---|---|
> | Monthly price | $0 | $29 | $99 |
> | Annual price (per month) | $0 | $23 | $79 |
> | Description | For individuals and small projects | For growing teams that need more power | For large teams with advanced needs |
> | CTA | "Get started free" | "Start free trial" | "Contact sales" |
>
> **Features per tier (use checkmarks ✓ and crosses ✗):**
> - Starter: Up to 3 projects ✓, 5 team members ✓, 5GB storage ✓, Basic integrations ✓, AI features ✗, Priority support ✗, Custom domain ✗, SLA ✗
> - Pro: Unlimited projects ✓, 25 team members ✓, 100GB storage ✓, All integrations ✓, AI features ✓, Priority support ✓, Custom domain ✗, SLA ✗
> - Enterprise: Unlimited projects ✓, Unlimited members ✓, 1TB storage ✓, All integrations ✓, AI features ✓, Priority support ✓, Custom domain ✓, SLA ✓
>
> **Visual style:**
> - Background: `#0a0a0f` (dark)
> - Card background: `#12121a`
> - Card border: `rgba(255,255,255,0.08)`
> - Accent/highlight: gradient `#7c3aed` → `#2563eb`
> - The Pro card has an accent gradient border and a "Most Popular" badge at the top
> - Body text: `#94a3b8`
> - Heading text: `#ffffff`
> - Checkmark color: `#7c3aed`
> - Cross color: `#475569`
> - Font: system-ui stack
>
> **Billing toggle behavior:**
> - Switching between Monthly/Annual animates the price numbers (fade out old → fade in new)
> - Annual prices display the discounted monthly rate prominently, with the regular monthly price shown with a strikethrough for comparison (e.g., "~~$29~~ $23/mo")
> - The "Save 20%" badge only appears when Annual is selected
>
> **Pro card highlight:**
> - Slightly larger card (scale or padding difference)
> - Gradient border using a pseudo-element or `border-image`
> - "Most Popular" badge at the top center in gradient colors
> - CTA button uses the accent gradient as background
>
> **FAQ accordion:**
> 4 questions:
> 1. "Can I change my plan later?" — Yes, you can upgrade or downgrade at any time. Changes take effect on your next billing cycle.
> 2. "Is there a free trial?" — Yes, all paid plans include a 14-day free trial. No credit card required.
> 3. "What payment methods do you accept?" — We accept all major credit cards, PayPal, and bank transfers for Enterprise plans.
> 4. "Do you offer discounts for nonprofits?" — Yes, we offer 50% off for registered nonprofits and educational institutions. Contact us to apply.
>
> Each accordion item has a smooth expand/collapse animation. Only one item can be open at a time.
>
> **CTA buttons:**
> - Hover: `translateY(-2px)` lift effect
> - "Contact sales" button is outlined/ghost style
>
> **Responsive:**
> - At < 768px, pricing cards stack vertically

## Reference Materials

None — text-only prompt. All specifications are self-contained.

## Evaluation Checklist

- [ ] Opens in a browser without errors
- [ ] Three pricing cards are displayed side by side
- [ ] Monthly/Annual billing toggle is present and functional
- [ ] Prices update correctly when toggling billing period
- [ ] Annual prices show the discounted amount and original price with strikethrough
- [ ] "Most Popular" / Pro card is visually distinguished from the others
- [ ] Feature lists show checkmarks and crosses for each tier
- [ ] FAQ accordion expands and collapses smoothly
- [ ] Only one FAQ item can be open at a time
- [ ] Overall dark theme matches the color specification
- [ ] Pro card CTA button uses the accent gradient
- [ ] Cards stack vertically below 768px
- [ ] No external CSS libraries or JS frameworks used

## Notes for Evaluators

**This evaluation tests interactive UI component skills.** A pricing table is one of the most common UI patterns in SaaS products — it tests whether a model can build a real, shippable component.

**Common failure modes**:
- Toggle switch built as two buttons rather than an animated pill toggle
- Annual price animation (fade in/out) is skipped — just immediate swap
- Strikethrough original price is often forgotten
- FAQ accordion may not enforce "only one open at a time"
- Pro card gradient border is commonly done with a plain colored border instead
- Responsive stacking is frequently omitted

**What "close enough" means**: If the three-tier pricing structure is clear, the billing toggle works, the feature lists are accurate, and the page is visually dark/professional, that's a strong pass. The accordion and animations are bonuses — a page without them but with correct pricing logic still earns partial credit.
