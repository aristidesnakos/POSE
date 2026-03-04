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
4. Run the generated output
5. Walk through the **Evaluation Checklist** — check each item pass/fail
6. Note which items passed and which failed

That's it. No infrastructure, no CI pipeline, no framework to install.

## Evaluation Checklists

Each prompt includes a checklist of 5-10 concrete, observable criteria. These are binary (pass/fail) to keep evaluation fast and consistent.

Checklist items fall into these categories:

| Category | What It Tests | Example |
|----------|--------------|---------|
| **Execution** | Does it run at all? | "Script executes without errors" |
| **Functional** | Does it do what was asked? | "Extracts all 5 required fields" |
| **Data Quality** | Is the output correct and clean? | "Numeric fields are numbers, not strings" |
| **Edge Cases** | Does it handle the unexpected? | "Handles missing salary field gracefully" |
| **Robustness** | Does it fail gracefully? | "Retries on timeout, logs errors" |

## Complexity Levels

Prompts are tagged by expected output complexity:

- **Simple** (< 200 LOC): Single function or straightforward script
- **Medium** (200-800 LOC): Multi-function script with error handling and data processing
- **Complex** (800+ LOC): Full application with UI, state management, or multi-component architecture

## Supported AI Tools

POSE prompts are designed to be tool-agnostic. They work with:

- **Chat interfaces**: ChatGPT, Claude, Gemini
- **AI code editors**: Cursor, Windsurf, Cline
- **App builders**: Lovable, Bolt.new, Same.dev
- **CLI agents**: Claude Code, Aider, Codex

The same prompt may produce different results in different tools — that's part of what POSE helps you evaluate.
