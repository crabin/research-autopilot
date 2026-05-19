# Academic Research Routing

Use this routing when `research-autopilot` is triggered and the request is not
only executable experiment automation.

| User intent | Capability |
| --- | --- |
| Run or automate code experiments in a repository | Research Autopilot core workflow |
| Turn a codebase into an autonomous experiment loop | Research Autopilot core workflow |
| Design a literature search, evidence synthesis, fact check, PRISMA review, systematic review, meta-analysis, or research question | Bundled `deep-research` |
| Write, outline, revise, format, or citation-check an academic paper | Bundled `academic-paper` |
| Review a manuscript, simulate peer review, critique methodology, or verify revisions | Bundled `academic-paper-reviewer` |
| Coordinate research -> paper -> integrity -> review -> revision -> finalization | Bundled `academic-pipeline` |

Bundled skill entrypoints live under:

- `references/academic-research-skills/deep-research/SKILL.md`
- `references/academic-research-skills/academic-paper/SKILL.md`
- `references/academic-research-skills/academic-paper-reviewer/SKILL.md`
- `references/academic-research-skills/academic-pipeline/SKILL.md`

For ML research projects, use the core workflow for reproducible experiment
entrypoints, metric contracts, and baseline commands before moving to paper
writing or review.

Load only the selected bundled skill's `SKILL.md` first. Defer agent prompts,
templates, scripts, and detailed references until that mode requires them.

Preserve upstream attribution when publishing: the vendored suite includes
`references/academic-research-skills/LICENSE` and
`references/academic-research-skills/NOTICE.md`.
