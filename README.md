# research-autopilot

`research-autopilot` is a reusable agent skill for turning a research codebase into an autonomous experimentation workflow.

It inspects a target repository, identifies the real experiment entrypoints and metrics, and generates project-specific files such as:

- `program.md`
- `results.tsv`
- thin wrapper `prepare.py`
- thin wrapper `train.py`
- cross-agent prompt templates

The skill is designed for ML and research repositories where the agent must read the code first, then generate automation files that match the project's real workflow instead of a generic template.

## What It Does

The skill helps an agent:

1. inspect the target research repository
2. identify setup steps and experiment entrypoints
3. verify output contracts and success metrics
4. decide whether wrapper `prepare.py` or `train.py` files are needed
5. generate a repository-specific `program.md`
6. generate experiment tracking files such as `results.tsv`

This is especially useful for:

- GAN or diffusion research pipelines
- classifier evaluation pipelines
- data augmentation research
- repositories with many partial scripts but no single automation entrypoint
- projects that need agent-friendly setup and experiment contracts

## Repository Layout

```text
SKILL.md
agents/openai.yaml
references/
  program-template.md
  claude-code-template.md
  examples/autoresearch/
```

Key files:

- `SKILL.md`: main skill instructions
- `references/program-template.md`: reusable `program.md` template guidance
- `references/claude-code-template.md`: plain prompt template for Claude Code and similar agents
- `references/examples/autoresearch/`: minimal worked example using bundled `prepare.py`, `train.py`, and `program.md`

## Installation

### Codex

If you want to install from GitHub into a compatible skills manager:

```bash
npx skills add https://github.com/crabin/research-autopilot
```

### SkillHub

Once indexed by SkillHub, the expected install form is:

```bash
npx skillhub install crabin/research-autopilot
```

### Claude Code

Claude Code does not automatically load Codex skills from this repository structure, but it can still use the generated files directly.

Recommended approach:

1. use this repository as the source skill definition
2. generate `program.md`, `prepare.py`, `train.py`, or prompts for the target project
3. let Claude Code read those generated files inside the target project

## Example Workflow

Given a research repository, the skill should:

1. read the repository README and actual training scripts
2. discover setup requirements and outputs
3. determine whether the repository already has usable `prepare.py` and `train.py` entrypoints
4. generate missing wrappers if needed
5. generate a project-specific `program.md`

The bundled `autoresearch` example shows a minimal version of this pattern.

## Notes for Marketplaces

This repository is a single-skill repository with the skill rooted at `SKILL.md`.

If a marketplace indexes public GitHub repositories containing `SKILL.md`, this repository is intended to be directly discoverable from:

- `crabin/research-autopilot`

## License

MIT
