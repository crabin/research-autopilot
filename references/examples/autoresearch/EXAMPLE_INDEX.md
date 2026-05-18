# Autoresearch Example Index

This folder contains a minimal reference implementation of the autonomous research pattern.

Read files in this order:

1. `README.md`
2. `program.md`
3. `prepare.py`
4. `train.py`

Use this example to understand:

- how a repo defines one fixed preparation script
- how one main experiment file is left editable
- how an agent-facing `program.md` defines the experiment loop
- how a fixed metric and a short experiment cycle enable keep/discard decisions
- how `prepare.py` exposes a clear ready signal
- how `train.py` exposes stable summary fields for automated parsing

Do not assume future target repositories should copy this structure exactly. Use it as a minimal worked example, then adapt to the target repo after inspecting its real code.
