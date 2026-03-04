# POSE — Practical One-Shot Evaluations

**Can an AI model produce something you'd actually ship from a single prompt?**

POSE is a curated collection of one-shot prompt specifications with pass/fail evaluation checklists. Each prompt is a real-world task you can copy-paste into any AI tool — then use the checklist to evaluate the result.

No framework to install. No CLI. No infrastructure. Just prompts, checklists, and honest assessment.

## How It Works

1. Pick a prompt from the table below
2. Copy the **Prompt** section into your AI tool (Cursor, Claude Code, ChatGPT, Lovable, Bolt.new, etc.)
3. Run the generated output
4. Walk through the **Evaluation Checklist** — check each item pass/fail

See [METHODOLOGY.md](METHODOLOGY.md) for details on the evaluation approach.

## Evaluations

### Scraping & Data Pipelines (Crawl4AI)

| Evaluation | Complexity | Checklist Items | What It Tests |
|-----------|-----------|----------------|--------------|
| [Job Listings Scraper](prompts/scraping-pipelines/crawl4ai-job-listings.md) | Medium | 10 | Structured extraction, pagination, LLM strategy |
| [E-commerce Price Monitor](prompts/scraping-pipelines/crawl4ai-ecommerce-prices.md) | Medium | 10 | CSS extraction, data normalization, CSV output |
| [News Aggregator](prompts/scraping-pipelines/crawl4ai-news-aggregator.md) | Complex | 11 | Multi-source concurrent crawling, deduplication |
| [Real Estate Listings](prompts/scraping-pipelines/crawl4ai-real-estate.md) | Medium | 10 | Messy data handling, dual output formats |
| [Competitor Monitor](prompts/scraping-pipelines/crawl4ai-competitor-monitor.md) | Complex | 11 | Real-world HTML diversity, date parsing, reporting |

### Web Tools

| Evaluation | Complexity | Checklist Items | What It Tests |
|-----------|-----------|----------------|--------------|
| [Break-Even Calculator](prompts/web-tools/break-even-calculator.md) | Medium | 10 | Image interpretation, chart rendering, financial logic |

### Interactive Apps

| Evaluation | Complexity | Checklist Items | What It Tests |
|-----------|-----------|----------------|--------------|
| [Kanjimon Memory Palace](prompts/interactive-apps/kanjimon-memory-palace.md) | Complex | 18 | Canvas game, state management, educational design |

## Why Scraping First?

Web scraping is universally needed, immediately testable, and reveals a lot about model capability:
- Can it use a specific library (Crawl4AI) correctly?
- Can it handle real-world HTML structures that vary across sites?
- Can it produce clean, structured data from messy input?
- Can it handle failures gracefully?

These skills transfer directly to any data pipeline or integration work.

## Contributing

Want to add an evaluation? Use the [prompt template](templates/prompt-template.md) and submit a PR. Each evaluation needs:
- A clear, self-contained prompt
- An evaluation checklist with 5-10 concrete pass/fail items
- Notes for evaluators on common failure modes

## Related Projects

- [Crawl4AI](https://github.com/unclecode/crawl4ai) — The scraping library used in our pipeline evaluations
- [Inspect AI](https://github.com/UKGovernmentBEIS/inspect_ai) — Comprehensive eval infrastructure (different approach — POSE is deliberately simpler)
- [Promptfoo](https://github.com/promptfoo/promptfoo) — Systematic prompt testing CLI
- [Vibe Code Bench](https://www.vals.ai/benchmarks/vibe-code) — Automated app generation evaluation

## License

MIT
