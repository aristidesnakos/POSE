# POSE — Practical One-Shot Evaluations

**Can an AI model build something you'd actually ship — from a single prompt?**

POSE is a curated collection of one-shot prompt specifications with pass/fail evaluation checklists, focused on **frontend and UI/UX** tasks. Each prompt is a real-world design or interaction challenge you can copy-paste into any AI tool — then use the checklist to honestly assess the result.

No framework to install. No CLI. No infrastructure. Just prompts, checklists, and honest assessment.

## Who Is This For?

POSE is aimed at **frontend developers, designers, and product builders** who want to know:

- Can this model produce a UI component that I'd actually put in my codebase?
- Can it build a playable HTML game from scratch in one shot?
- Can it turn a wireframe or a design brief into working, styled HTML?

The evaluations live in the space between static mockups and full-stack apps: **interactive, functional, visually intentional — but self-contained** (a single HTML file or a lightweight script, with no complicated backend).

## How It Works

1. Pick a prompt from the table below
2. Copy the **Prompt** section into your AI tool (Cursor, Claude Code, ChatGPT, Lovable, Bolt.new, etc.)
3. Open the generated output in a browser (or run it)
4. Walk through the **Evaluation Checklist** — check each item pass/fail

See [METHODOLOGY.md](METHODOLOGY.md) for details on the evaluation approach and scoring criteria.

## Evaluations

### UI Components

Ship-ready interface components: landing pages, dashboards, pricing sections — the building blocks of real products.

| Evaluation | Complexity | Checklist Items | What It Tests |
|-----------|-----------|----------------|--------------|
| [SaaS Hero Section](prompts/ui-components/hero-section.md) | Medium | 13 | Visual design, CSS animation, responsive layout, brand consistency |
| [Pricing Table](prompts/ui-components/pricing-table.md) | Medium | 13 | Interactive toggle, conditional rendering, visual hierarchy |

### HTML Games

Self-contained browser games: the ultimate test of logic, physics, and interactive design in a single file.

| Evaluation | Complexity | Checklist Items | What It Tests |
|-----------|-----------|----------------|--------------|
| [Snake Game](prompts/html-games/snake-game.md) | Medium | 15 | Game loop, collision detection, canvas rendering, localStorage |
| [Flappy Bird Clone](prompts/html-games/flappy-bird.md) | Medium | 14 | Physics simulation, procedural generation, multi-state management |
| [Kanjimon Memory Palace](prompts/interactive-apps/kanjimon-memory-palace.md) | Complex | 18 | Canvas game, state management, educational design |

### Web Tools

Functional mini-apps with real utility — calculators, dashboards, data visualizations.

| Evaluation | Complexity | Checklist Items | What It Tests |
|-----------|-----------|----------------|--------------|
| [Break-Even Calculator](prompts/web-tools/break-even-calculator.md) | Medium | 10 | Image interpretation, chart rendering, financial logic |

### Scraping & Data Pipelines

Backend-leaning evaluations for teams that need data extraction and processing skills.

| Evaluation | Complexity | Checklist Items | What It Tests |
|-----------|-----------|----------------|--------------|
| [Job Listings Scraper](prompts/scraping-pipelines/crawl4ai-job-listings.md) | Medium | 10 | Structured extraction, pagination, LLM strategy |
| [E-commerce Price Monitor](prompts/scraping-pipelines/crawl4ai-ecommerce-prices.md) | Medium | 10 | CSS extraction, data normalization, CSV output |
| [News Aggregator](prompts/scraping-pipelines/crawl4ai-news-aggregator.md) | Complex | 11 | Multi-source concurrent crawling, deduplication |
| [Real Estate Listings](prompts/scraping-pipelines/crawl4ai-real-estate.md) | Medium | 10 | Messy data handling, dual output formats |
| [Competitor Monitor](prompts/scraping-pipelines/crawl4ai-competitor-monitor.md) | Complex | 11 | Real-world HTML diversity, date parsing, reporting |

## What Makes a Great POSE Evaluation?

The best evaluations are tasks where the bar is immediately obvious:

- **You can see it** — open a browser and the result either looks good or it doesn't
- **You can use it** — click buttons, play the game, enter data
- **You can compare it** — side-by-side with the spec or your mental model of "good"

UI components and HTML games meet all three criteria. You know within 10 seconds whether the model produced something shippable.

## Contributing

Want to add an evaluation? Use the [prompt template](templates/prompt-template.md) and submit a PR. Each evaluation needs:
- A clear, self-contained prompt
- An evaluation checklist with 5-15 concrete pass/fail items
- Notes for evaluators covering common failure modes and what "close enough" means

Good candidates: landing page sections, dashboard widgets, data visualizations, browser games, interactive forms, animation showcases.

## Related Projects

- [Inspect AI](https://github.com/UKGovernmentBEIS/inspect_ai) — Comprehensive eval infrastructure (different approach — POSE is deliberately simpler)
- [Promptfoo](https://github.com/promptfoo/promptfoo) — Systematic prompt testing CLI
- [Vibe Code Bench](https://www.vals.ai/benchmarks/vibe-code) — Automated app generation evaluation
- [Crawl4AI](https://github.com/unclecode/crawl4ai) — The scraping library used in our pipeline evaluations

## License

MIT
