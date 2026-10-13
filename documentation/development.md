# Development guide

Notes for developers working in this repository. Consumers need only the
project README at the repository root.

## Related projects

- `python-project-common` — Python Copier template and project tooling.
- `rust-project-common` — Rust Copier template; links out to this site,
  ships no documentation tree.
- `agents-common` — agent configurations; consumes staged guides via
  `agentsmgr populate`.

## Repository layout

- `documentation/` — Sphinx site sources (Markdown with MyST).
- `documentation/architecture/` — architecture notes and OpenSpec home
  (interim; OpenSpec workflow is described in
  `.auxiliary/agents/procedures/openspec.md`).
- `openspec/` — symlink to the OpenSpec home above.

## Building the documentation

Prerequisites: `uv` and the Sphinx dependencies (`sphinx`, `furo`,
`myst-parser`, `sphinx-copybutton`, `sphinx-inline-tabs`).

Build HTML into the ignored scratch directory (never commit build output):

```sh
uv run --with sphinx --with furo --with myst-parser \
    --with sphinx-copybutton --with sphinx-inline-tabs \
    sphinx-build -b html documentation .auxiliary/temporary/sphinx-build
```

The build must complete with zero warnings.

## Workflow

- Design discussion goes through OpenSpec changes; implementation is gated
  behind Tier-1/Tier-2 review plus operator approval — see
  `.auxiliary/agents/procedures/`.
- Use `--fixup` commits for review feedback, held unsquashed until final
  approval, then autosquashed. See the delegated review procedure.
- Coordination notes live in the `documentation-common` notebook.
- This repository is not a Copier template consumer: never run
  `copier update` here.
