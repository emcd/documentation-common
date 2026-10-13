# documentation/

Sphinx site sources for `documentation-common`. Surgically copied from the
`python-project-common` Copier template (`template/documentation/`), not
instantiated from it: this repository is not a Copier template consumer, so
`copier update` must never be run here.

## Sync checklist

When the template revs docs tooling, diff these files against
`template/documentation/` upstream and port deliberately:

- `conf.py` — extensions, theme, MyST config, `linkcheck_ignore`
- `index.rst` — toctree structure

Deliberate divergences from the template (do not "sync" these away):

- No `_import_version()` — no Python package; static `release`/`version`.
- No Copier-injected intersphinx foundations and no `nitpick_ignore` entries
  for a local package.
- `linkcheck_ignore` targets `emcd/documentation-common`, not a template URI.
- `common/` holds the migrated guides at URL cutover
  (`migrate-shared-docs-urls`); `architecture/` stays excluded from the build.
