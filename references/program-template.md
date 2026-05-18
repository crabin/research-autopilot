# Program Template

Use this as a starting shape, then adapt it to the target repository after reading real code.

## Goal

State the actual research objective in one to three lines.

Include:

- primary metric
- secondary metrics
- what does not count as success

## Scope

List:

- editable files
- non-editable files
- any files that require special caution

## Setup

State:

- which preparation steps must happen before the first experiment
- whether the repository already has a usable `prepare.py` or equivalent
- if not, whether a thin wrapper `prepare.py` should be generated
- how to verify setup is complete

## Baseline Command

Record the canonical baseline experiment command exactly as supported by the repository.

If the repository lacks a single training entrypoint, define or generate a thin `train.py` wrapper around the real project scripts.

## Output Files

List the result artifacts to inspect after each run, for example:

- `metrics.json`
- `generation_quality.json`
- `config.json`
- `class_report.csv`
- `confusion_matrix.csv`

Also state the required output contract:

- which fields must be printed to stdout
- which files must exist after the run
- which metric is the source of truth for keep/discard decisions

## Success Criteria

Rank metrics in decision order. Prefer a deterministic tie-break rule.

## Logging

If useful, define a flat `results.tsv` schema with only the fields needed for comparison.

## Experiment Loop

Write a short, explicit loop:

1. inspect git state
2. make one focused change
3. run experiment
4. inspect outputs
5. log result
6. keep or discard

## Crash Handling

Specify when to retry, when to fix obvious bugs, and when to abandon a bad idea.

## First Run

Require a baseline run before optimization.

## Wrapper Rules

If you generate `prepare.py` or `train.py`:

- keep them thin and reusable
- call existing project code instead of duplicating it
- preserve the project's real evaluation logic
- print stable, parseable status lines
