# POSE Methodology

## What "One-Shot" Means

A one-shot evaluation gives an AI model a single prompt and evaluates the output without iterative refinement. The user copies the prompt, pastes it into an AI tool, and assesses the result against a checklist.

This mirrors how practitioners actually test models: you give it a task, see what comes back, and decide if it's usable.

### One-Shot vs. One-Prompt

- **One-shot**: The model generates output in a single pass (e.g., pasting into ChatGPT or a Lovable-style builder)
- **One-prompt**: The user gives one instruction, but the model/agent may take multiple actions internally (e.g., Cursor, Claude Code, Cline). The user still only writes one prompt

POSE evaluations are designed to work in both modes. The prompt is the same — only the execution environment differs.

## How to Use POSE

1. Pick a prompt from the `prompts/` directory
2. Copy the entire **Prompt** section
3. Paste it into your AI tool of choice (Cursor, Claude Code, ChatGPT, Lovable, Bolt.new, etc.)
4. Open the generated output in a browser (or run it)
5. Walk through the **Evaluation Checklist** — check each item pass/fail
6. Note which items passed and which failed

That's it. No infrastructure, no CI pipeline, no framework to install.

## Evaluation Checklists

Each prompt includes a checklist of concrete, observable criteria. These are binary (pass/fail) to keep evaluation fast and consistent.

### General Checklist Categories

| Category | What It Tests | Example |
|----------|--------------|---------|
| **Execution** | Does it run at all? | "Opens in a browser without errors" |
| **Functional** | Does it do what was asked? | "Billing toggle switches between monthly and annual prices" |
| **Data Quality** | Is the output correct and clean? | "Break-even calculation is mathematically correct" |
| **Edge Cases** | Does it handle the unexpected? | "Snake cannot reverse direction" |
| **Robustness** | Does it fail gracefully? | "Game restarts cleanly after game over" |

### UI/UX-Specific Checklist Categories

For UI components and HTML games, checklists also cover:

| Category | What It Tests | Example |
|----------|--------------|---------|
| **Visual Accuracy** | Does it match the design spec? | "Gradient text uses the specified accent colors" |
| **Design Quality** | Does it look intentional and professional? | "Pro card is visually distinguished from other tiers" |
| **Interactivity** | Do all interactions work? | "FAQ accordion expands and collapses smoothly" |
| **Animation** | Are motion details correct? | "Mockup card floats with a continuous animation" |
| **Responsive** | Does it adapt to screen size? | "Cards stack vertically below 768px" |
| **Constraint Adherence** | Did the model stay within bounds? | "No external CSS libraries or JS frameworks used" |

## Complexity Levels

Prompts are tagged by expected output complexity:

- **Simple** (< 200 LOC): Single function or straightforward script
- **Medium** (200-800 LOC): Multi-function script or component with interactivity and styling
- **Complex** (800+ LOC): Full application with multiple states, game logic, or multi-component architecture

## What Makes a Good One-Shot UI Evaluation?

The best UI evaluations share three properties:

1. **Immediately assessable** — You can open the output in a browser and judge quality within 10 seconds
2. **Concretely specified** — The prompt is detailed enough that "close enough" has a clear meaning
3. **Meaningfully functional** — It does something, not just looks like something (buttons work, games play, toggles toggle)

### The "Would You Ship It?" Test

After completing the binary checklist, ask one final question: *could this output be used in a real product with minimal changes?* This is a supplemental qualitative signal, separate from the checklist score. A high checklist score is the primary measure of quality — the "ship it" question is a secondary gut-check for cases where the output looks great but misses a few low-weight items, or passes all checklist items but looks visually incoherent.

## Supported AI Tools

POSE prompts are designed to be tool-agnostic. They work with:

- **Chat interfaces**: ChatGPT, Claude, Gemini
- **AI code editors**: Cursor, Windsurf, Cline
- **App builders**: Lovable, Bolt.new, Same.dev
- **CLI agents**: Claude Code, Aider, Codex

The same prompt may produce very different results in different tools — that's part of what POSE helps you evaluate. A UI prompt run in Lovable (which renders output immediately) versus Claude's chat interface reveals very different strengths and failure modes.

