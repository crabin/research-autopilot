---
name: research-autopilot
description: Analyze a research codebase, identify its real experiment entrypoints, metrics, and editable scope, then generate project-specific automation files such as `program.md`, `results.tsv`, or experiment prompts. Use when a user wants to adapt autonomous research workflows to a local research repository, especially ML/GAN/classifier pipelines where the agent must inspect code before proposing or generating files.
---

# Research Autopilot

Inspect the target repository before proposing any automation workflow. Do not assume the project matches a generic template.

## Core Workflow

Follow this sequence:

1. Locate the repository root the user wants to automate.
2. Read the minimal files needed to understand the real workflow:
   - root `README`
   - experiment or training entry scripts
   - config files
   - evaluation or metrics output logic
   - any existing sweep or pipeline scripts
3. Determine:
   - the main experiment entrypoint
   - whether the repository already has a usable preparation/setup entrypoint
   - whether the repository already has a usable training entrypoint
   - whether the project trains a model, runs a pipeline, or only evaluates
   - which metrics actually decide success
   - which files are safe for an autonomous agent to edit
   - which files should stay fixed
   - where outputs are written
   - whether the current scripts expose enough information for autonomous keep/discard decisions
4. Reduce the project to a controllable automation loop.
5. Generate the project-specific files the user needs.

If the repository does not already provide a clean setup entrypoint or training entrypoint, generate thin wrapper scripts such as `prepare.py` and `train.py` that call existing project scripts. Prefer wrapping existing logic over reimplementing it.

## Output Rules

Generate only files that materially help automation. The common outputs are:

- `program.md`
- `results.tsv` or a `results.tsv` template
- `prepare.py` when the repo lacks a single reusable setup/preparation entrypoint
- `train.py` when the repo lacks a single reusable training/evaluation entrypoint
- a short baseline command
- a prompt template for non-Codex agents

When generating `program.md`, include:

- the project goal
- setup and readiness checks
- primary and secondary success metrics
- editable and non-editable file scope
- the baseline experiment command
- the result files to inspect
- the output fields or files required after each run
- the keep/discard decision rule
- crash handling
- a requirement to establish baseline first

## Repository Analysis Heuristics

Prefer concrete code evidence over documentation claims.

Use these heuristics:

- If the repo has a single orchestration script, use that as the main entrypoint.
- If the repo has many partial scripts but no single canonical setup command, create a thin `prepare.py` wrapper that performs the required preparation sequence.
- If the repo has many partial scripts but no single canonical experiment command, create a thin `train.py` wrapper that performs the required training plus metric export sequence.
- If metrics are written to `metrics.json`, `results.json`, or CSV reports, prefer those over console logs.
- If metrics are only printed in free-form logs, require a stable summary section or write structured outputs from the wrapper.
- If the project has separate generation and classifier phases, optimize for the downstream task metric, not generation realism alone.
- If the project contains sweep scripts, use them to discover accepted CLI arguments, canonical output paths, and existing score formulas.
- If many files exist, restrict the editable scope to the smallest set that can influence the target behavior.

## Setup and Output Contract Checks

Before generating automation files, verify these questions from code:

1. Is there a reproducible setup step for data, preprocessing, tokenizers, weights, or caches?
2. Can the setup step be checked cheaply, for example by verifying expected files or directories?
3. Is there a single training command that another agent can run repeatedly?
4. Does the training flow emit stable machine-readable outputs or at least stable summary lines?
5. Is there a clear success metric and enough context to compare two runs?

If any answer is no, generate the missing wrapper or contract.

For `prepare.py`, prefer a wrapper that:

- runs the minimal required setup steps in the correct order
- prints clear readiness messages
- fails fast when prerequisites are missing
- ends with an explicit ready signal

For `train.py`, prefer a wrapper that:

- runs the project's real training or pipeline logic
- preserves the real metric source of truth
- emits stable summary lines and or structured files needed for automation
- exits non-zero on failure

Do not invent fake metrics. Only surface real outputs already computed by the project or by a faithful wrapper around its existing evaluation.

## Metric Selection

Choose metrics that match the research objective.

Examples:

- Imbalanced classification: prefer `minority_f1`, per-class F1, `macro_f1`
- Generative augmentation for classifiers: prefer downstream classifier gains first, generation quality second
- Pure generative modeling: prefer the repository's fixed evaluation metric

Do not optimize only for accuracy when the project is explicitly about imbalance or minority classes.

## File Generation Guidance

For `program.md`:

- write it for another agent, not for the human
- use imperative instructions
- constrain scope tightly
- include an explicit setup phase before the experiment loop
- define a concrete experiment loop
- state exactly how to verify setup completion
- state exactly which outputs must exist after each run

For `results.tsv`:

- include only the metrics needed for keep/discard decisions
- keep the schema flat and easy to append to

For generated `prepare.py` and `train.py` wrappers:

- keep them thin
- call existing repository scripts or modules whenever possible
- document the source script they wrap
- print stable, parseable status information

For cross-agent reuse:

- write prompts and templates in plain Markdown so Claude Code and similar agents can read them directly
- do not rely on Codex-only mechanics inside those templates

## Cross-Agent Compatibility

Codex can use this skill directly. Other agents such as Claude Code cannot automatically load Codex skills, so also generate plain files they can read.

When the user asks for cross-agent reuse:

1. Generate the normal project files in the target repo.
2. If useful, also generate a plain prompt file such as `agent_prompt.md` or `program.md`.
3. Keep the instructions self-contained and avoid references to hidden skill behavior.

## References

Read [references/program-template.md](references/program-template.md) when you need a reusable structure for `program.md`.

Read [references/claude-code-template.md](references/claude-code-template.md) when the user wants a prompt/template that Claude Code or other agents can use directly.

Read [references/examples/autoresearch/README.md](references/examples/autoresearch/README.md) plus the bundled example files in `references/examples/autoresearch/` when you want a concrete minimal example of this workflow in a real repository.
