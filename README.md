# POSE — Practical One-Shot Evaluations

**Can an AI model build something you'd actually ship — from a single prompt?**

POSE is a curated collection of one-shot prompt specifications with pass/fail evaluation checklists, focused on **frontend and UI/UX** tasks. Each prompt is a real-world design or interaction challenge you can copy-paste into any AI tool — then use the checklist to honestly assess the result.

No framework to install. No CLI. No infrastructure. Just prompts, checklists, and honest assessment.

## Who Is This For?

POSE is aimed at **frontend developers, designers, and product builders** who want to know:

- Can this model produce a UI component that I'd actually put in my codebase?
- Can it build a playable HTML game from scratch in one shot?
- Can it turn a wireframe or a design brief into working, styled HTML?

The evaluations live in the space between static mockups and full-stack apps: **interactive, functional, visually intentional — but self-contained** (a single HTML file, with no complicated backend).

## How It Works

1. Pick a prompt from the table below
2. Copy the **Prompt** section into your AI tool (Cursor, Claude Code, ChatGPT, Lovable, Bolt.new, etc.)
3. Open the generated output in a browser
4. Walk through the **Evaluation Checklist** — check each item pass/fail

See [METHODOLOGY.md](METHODOLOGY.md) for details on the evaluation approach and scoring criteria.

## Evaluations

### UI Components

| Evaluation | Complexity | Checklist Items | What It Tests |
|-----------|-----------|----------------|--------------|
| [SaaS Hero Section](prompts/ui-components/hero-section.md) | Medium | 13 | Visual design, CSS animation, responsive layout |

### HTML Games

| Evaluation | Complexity | Checklist Items | What It Tests |
|-----------|-----------|----------------|--------------|
| [Snake Game](prompts/html-games/snake-game.md) | Medium | 15 | Game loop, collision detection, canvas rendering, localStorage |
| [Kanjimon Memory Palace](prompts/interactive-apps/kanjimon-memory-palace.md) | Complex | 18 | Canvas game, state management, educational design, pixel art |

### Web Tools

| Evaluation | Complexity | Checklist Items | What It Tests |
|-----------|-----------|----------------|--------------|
| [Break-Even Calculator](prompts/web-tools/break-even-calculator.md) | Medium | 10 | Chart rendering, financial logic, image interpretation |

More evaluations are planned and will be added incrementally — pricing tables, dashboard widgets, more games, and data visualizations.

## Running with EvalPulse

POSE evaluations can be run automatically against multiple models using [EvalPulse](https://github.com/aristidesnakos/model-evals-framework) — a lightweight pipeline that scores LLM outputs with dual-judge evaluation and generates comparison reports.

The `evals/` folder contains ready-to-use EvalPulse suites:

| Suite | Evaluations included |
|-------|---------------------|
| [`evals/pose-ui.json`](evals/pose-ui.json) | SaaS Hero Section, Snake Game |

**Quick start:**

```bash
# Clone EvalPulse
git clone https://github.com/aristidesnakos/model-evals-framework
cd model-evals-framework

# Install and configure
pip install -r requirements.txt
cp .env.example .env  # add your OpenRouter API key

# Copy the POSE suite into EvalPulse
cp /path/to/POSE/evals/pose-ui.json evals/

# Dry-run to verify the pipeline
python evalpulse.py --dry-run --suite pose_ui

# Full evaluation across all enabled models
python evalpulse.py --run-eval --suite pose_ui --dashboard
```

## What Makes a Great POSE Evaluation?

The best evaluations are tasks where the bar is immediately obvious:

- **You can see it** — open a browser and the result either looks good or it doesn't
- **You can use it** — click buttons, play the game, enter data
- **You can compare it** — side-by-side with the spec or your mental model of "good"

## Contributing

Want to add an evaluation? Use the [prompt template](templates/prompt-template.md) and submit a PR. Each evaluation needs:
- A clear, self-contained prompt
- An evaluation checklist with 5-15 concrete pass/fail items
- Notes for evaluators covering common failure modes and what "close enough" means

Good candidates: landing page sections, dashboard widgets, browser games, interactive forms, data visualizations.

## Related Projects

- [EvalPulse](https://github.com/aristidesnakos/model-evals-framework) — Automated multi-model evaluation pipeline (run POSE evals at scale)
- [Inspect AI](https://github.com/UKGovernmentBEIS/inspect_ai) — Comprehensive eval infrastructure (different approach — POSE is deliberately simpler)
- [Promptfoo](https://github.com/promptfoo/promptfoo) — Systematic prompt testing CLI
- [Vibe Code Bench](https://www.vals.ai/benchmarks/vibe-code) — Automated app generation evaluation

## License

MIT
