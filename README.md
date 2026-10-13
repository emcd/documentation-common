# documentation-common

Common documentation for all projects: language-neutral standards and
guidance, plus language-specific overlays. Canonical home for the guides
previously published from `python-project-common`.

Related projects:

- `python-project-common` — Python Copier template and project tooling;
  current canonical home of the common guides until URL cutover.
- `rust-project-common` — Rust Copier template; links out to this site,
  ships no documentation tree.
- `agents-common` — agent configurations; consumes staged guides via
  `agentsmgr populate`.

## Repository layout

- `documentation/` — Sphinx site sources (Markdown with MyST).
  `documentation/common/` lands the migrated guides at URL cutover.
- `openspec/` — OpenSpec proposals and specs
  (root `openspec/` is a symlink to `documentation/architecture/openspec/`).
- `documentation/architecture/` — architecture notes and OpenSpec home.

## Building the documentation

Prerequisites: `uv` and the Sphinx dependencies (`sphinx`, `furo`,
`myst-parser`, `sphinx-copybutton`, `sphinx-inline-tabs`).

Build HTML into the ignored scratch directory (never commit build output):

```sh
uv run --with sphinx --with furo --with myst-parser \
    --with sphinx-copybutton --with sphinx-inline-tabs \
    sphinx-build -b html documentation .auxiliary/temporary/sphinx-build
```

The build must complete with zero warnings. Two known-good patterns are
already handled: `documentation/_static/` is preserved via `.gitignore`
and the subsystem `documentation/README.md` is excluded from the build.

## Workflow

- Design discussion goes through OpenSpec changes; implementation is gated
  behind Tier-1/Tier-2 review plus operator approval — see
  `.auxiliary/agents/procedures/`.
- Coordination notes live in the `documentation-common` notebook
  (`coordination/maintainer_acceptance_and_migration_agenda`).
- This repository is not a Copier template consumer: never run
  `copier update` here.
