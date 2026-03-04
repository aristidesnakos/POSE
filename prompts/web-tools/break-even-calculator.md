# Break-Even Analysis Calculator

## Metadata
- **Category**: web-tools
- **Complexity**: Medium (200-800 LOC)
- **Output Type**: Single HTML file
- **Key Skills Tested**: Chart rendering, financial calculations, design-from-image interpretation, brand color extraction
- **Dependencies**: None (single HTML file with embedded JS)

## Prompt

> Create this break even analysis chart tool exactly as shown in the attached image. Please use brand colors from the Mercury Bank screenshot.

## Reference Materials

- ![Break Even Analysis Paper Napkin Image](/images/break-even-analysis-image.jpg) — Hand-drawn wireframe showing the expected chart layout and functionality
- ![Mercury Bank Screenshot](/images/mercury-bank-screenshot.png) — Reference for brand color palette

## Evaluation Checklist

- [ ] Opens in a browser without errors
- [ ] Renders an interactive break-even analysis chart
- [ ] Chart shows revenue line and cost line intersecting at break-even point
- [ ] Break-even point is visually highlighted or labeled
- [ ] User can input fixed costs, variable cost per unit, and price per unit
- [ ] Chart updates when inputs change
- [ ] Uses colors derived from the Mercury Bank screenshot (dark theme, purple/blue accents)
- [ ] Layout matches the general structure of the hand-drawn wireframe
- [ ] Break-even calculation is mathematically correct (fixed costs / (price - variable cost))
- [ ] Responsive or at minimum usable at standard desktop width

## Notes for Evaluators

**This evaluation tests image interpretation.** The prompt deliberately relies on attached images rather than text descriptions. The AI must:
1. Interpret a hand-drawn wireframe to understand layout and features
2. Extract a color palette from a screenshot of an existing product

**Common failure modes**:
- Model may not interpret the napkin sketch correctly — the chart type and axis labels may be wrong
- Color extraction from the Mercury screenshot may be approximate — that's fine as long as the overall feel is consistent
- Some models will use Chart.js or similar libraries (acceptable); others will use pure Canvas (also acceptable)
- Models may miss the interactive aspect — a static chart is only a partial pass

**What "close enough" means**: If it renders a break-even chart with correct math, accepts user input, and uses a dark/professional color scheme inspired by the reference, it's a pass. The layout doesn't need to be pixel-perfect to the wireframe.
