## Why

The static publisher (`sources/emcdproj/website.py:218-297` in python-project-common) sorts all versions via `packaging.Version` and is driven by `hatch version`, not git tags. A `docs-*` tag therefore cannot publish a `docs-2/` subtree today, blocking versioned shared-doc lines for documentation-common and its consumers.

## What Changes

- Introduce explicit publication tracks alongside existing `stable/` and `development/` aliases, including docs-line aliases (e.g. `docs-2/`).
- Generalize alias selection from hatch-version-driven to tag-driven, with old `stable`/`development` behavior regression-pinned.
- Require complete validated tree construction before alias promotion, retention of previous good output on source failure, and serialized concurrent publications.
- Preserve per-project release matrices/indexes and immutable historical trees; consume explicit configuration and never infer docs selection from PEP 440 package tags.
- No Copier template and no PyPI package move in this change; publisher stays in python-project-common until validated.

## Capabilities

### New Capabilities

- `publication-tracks`: explicit track definitions (stable, development, docs-line aliases), tag-namespace matching, and atomic alias promotion with rollback.
- `publisher-robustness`: validated-tree-before-promotion, failure retention, concurrent-publication serialization, and rebuild/replay semantics.

### Modified Capabilities

- None (no existing specs in documentation-common yet).

## Impact

- Affects python-project-common `emcdproj.website` publisher and its CI publication workflow.
- Unblocks the URL/source migration change (docs-2 aliases, compat mirror) which is gated on this change's staged proof.
- Acceptance: old-input→old-output equivalence proven, 36 legacy entrypoints validated, matrices preserved.
