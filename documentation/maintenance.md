# Maintenance

Notes for maintainers working in this repository. Consumers need only the
project README at the repository root.

## Repository layout

- `documentation/` — Sphinx site sources (Markdown with MyST).

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
