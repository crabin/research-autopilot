# Claude Code Prompt Template

Use this template when the user wants another agent such as Claude Code to execute the same workflow manually.

```md
Read the repository first before proposing changes.

Your task is to automate research for this project.

1. Read the repository root README.
2. Identify the true experiment entrypoint, output files, and evaluation metrics from code.
3. Identify the minimal set of files that should be editable during autonomous experiments.
4. Generate or update `program.md` so it matches this repository's real workflow.
5. If needed, generate a `results.tsv` template for experiment tracking.

Constraints:
- Do not assume this project matches a generic ML template.
- Prefer metrics written by the codebase over README claims.
- If the project optimizes data augmentation for classification, prioritize downstream classifier metrics over generation realism alone.
- Keep the editable scope as small as possible.
- Require a baseline run before iterative optimization.
```

Adapt the wording to the target project after inspection.
