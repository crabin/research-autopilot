# Research Autopilot

Research Autopilot is a Codex skill for executable research automation and
academic research workflows.

It has two layers:

1. Core experiment automation for research repositories.
2. A vendored Academic Research Skills suite for literature work, manuscript
   writing, manuscript review, and research-to-publication orchestration.

## Capabilities

### Research repository automation

Use this skill when a project needs to become a repeatable experiment loop.

It can:

- inspect a research codebase before proposing automation
- identify real setup, training, generation, evaluation, and sweep entrypoints
- determine the metric source of truth
- define editable and non-editable file scope
- generate `program.md`, `results.tsv`, `prepare.py`, `train.py`, and agent
  prompt templates when useful
- prefer thin wrappers around existing project logic over reimplementation
- surface stable outputs for autonomous keep/discard decisions

The default optimization target is the metric that matches the research goal.
For imbalanced classification and generative augmentation projects, this usually
means downstream or minority-class metrics rather than raw accuracy.

### Bundled academic workflows

The vendored suite lives in:

`references/academic-research-skills/`

It includes:

- `deep-research`: research question design, literature review, evidence
  synthesis, fact checking, systematic review, PRISMA, and meta-analysis.
- `academic-paper`: paper planning, outlining, drafting, revision, citation
  checks, formatting, abstracts, and disclosure workflows.
- `academic-paper-reviewer`: manuscript review, peer-review simulation,
  methodology critique, re-review, and reviewer calibration.
- `academic-pipeline`: end-to-end research -> paper -> integrity -> review ->
  revision -> finalization orchestration.

When network access is available, the academic workflow can search for papers
and verify references through web search and bibliographic indexes such as
Semantic Scholar, OpenAlex, and Crossref. A typical direction-setting pass is:
topic scoping -> paper search -> source screening -> citation verification ->
theme/gap synthesis -> candidate next research directions.

## Routing

Use the narrowest workflow that satisfies the request.

| Request | Route |
| --- | --- |
| Automate code experiments in a local repository | Core Research Autopilot |
| Build an autonomous experiment loop | Core Research Autopilot |
| Online paper search, literature review, fact check, PRISMA, meta-analysis, or research question design | Bundled `deep-research` |
| Paper outline, drafting, revision, citation checking, or formatting | Bundled `academic-paper` |
| Manuscript critique, peer-review simulation, methodology review, or re-review | Bundled `academic-paper-reviewer` |
| Full research-to-publication workflow | Bundled `academic-pipeline` |

For ML research projects, use both layers when needed: first establish
reproducible experiment commands and metric contracts, then use the academic
workflows for framing, writing, review, and publication.

## Usage Examples

```text
Use $research-autopilot to inspect this repository and create a program.md for autonomous experiments.
```

```text
Use $research-autopilot to design the literature review and research question for this ML augmentation project.
```

```text
Use $research-autopilot to help turn these verified experiment results into a paper outline.
```

```text
Use $research-autopilot to review this manuscript and produce a revision roadmap.
```

## Publication Notes

The skill is designed for progressive loading:

- load `SKILL.md` first
- read only the selected bundled academic skill's `SKILL.md`
- defer detailed agent prompts, templates, scripts, and references until needed

When publishing or redistributing this skill, preserve upstream attribution for
the vendored Academic Research Skills suite:

- `references/academic-research-skills/LICENSE`
- `references/academic-research-skills/NOTICE.md`

## License

The original Research Autopilot skill content is distributed under the
repository's top-level license. The vendored Academic Research Skills suite is
third-party content and remains governed by its own upstream license and notice
files under `references/academic-research-skills/`.

## Scope Boundary

This skill can support research automation and academic writing workflows, but
it should not fabricate data, invent metrics, invent citations, or bypass human
research judgment. Generated experiment wrappers should call real project logic,
and academic outputs should preserve source verification and citation integrity.
