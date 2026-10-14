## Why

The static publisher (`sources/emcdproj/website.py` in python-project-common) sorts all versions via `packaging.Version` and is driven by `hatch version`, not git tags. It therefore cannot publish tag-driven versioned documentation lines — floating-major aliases (e.g. `v1/` over `v1.*` releases) for documentation-common — nor select aliases from explicit configuration.

## What Changes

- Introduce explicit publication tracks alongside existing `stable/` and `development/` aliases, including floating-major aliases (e.g. `v1/`). No `docs-*` tag family: common documentation is versioned by documentation release lines, never by docs-specific tags.
- Generalize alias selection from hatch-version-driven to tag-driven, with old `stable`/`development` behavior regression-pinned.
- Require complete validated tree construction before alias promotion, retention of previous good output on source failure, and serialized concurrent publications.
- Preserve per-project release matrices/indexes and immutable historical trees; consume explicit configuration with kebab-case TOML keys per project TOML practices.
- No Copier template and no PyPI package move in this change; publisher stays in python-project-common until validated.

## Capabilities

### New Capabilities

- `publication-tracks`: explicit track definitions (stable, development, floating-major aliases), tag-namespace matching, and atomic alias promotion with rollback.
- `publisher-robustness`: validated-tree-before-promotion, failure retention, concurrent-publication serialization, and rebuild/replay semantics.

### Modified Capabilities

- None (no existing specs in documentation-common yet).

## Impact

- Affects python-project-common `emcdproj.website` publisher and its CI publication workflow.
- Unblocks the URL/source migration change (versioned canonical URLs, floating majors, compat mirror) which is gated on this change's staged proof.
- Acceptance: old-input→old-output equivalence proven, 36 legacy entrypoints validated, matrices preserved.
