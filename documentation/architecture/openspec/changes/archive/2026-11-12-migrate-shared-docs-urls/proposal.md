## Why

Shared docs live in python-project-common (`documentation/common/`, 36 stable links) with no versioned canonical home for documentation-common consumers. Rust generated-documentation links and agents ingestion need stable versioned targets, but cutover without compat would break baked links in every rendered consumer repo.

## What Changes

- Publish canonical versioned URLs (releases plus floating majors, no `docs-*` tag family) in documentation-common once the publisher-generalize change provides staged proof; gate this change on that acceptance.
- Keep compat mirror or redirects at old python-project-common `stable/sphinx-html/common/` paths beyond any known-sites link-sweep; sweep reduces dependence but never proves deletability.
- Update template assets to the new canonical URL only after compat is verified; filename-map updates in agents-common move atomically with the URL change.
- Hold ADR 003 anchor contract for the docs-major line; enforce explicit old-base→new-base mapping with fragment verification for any published-HTML link rewrite.
- Sunset revisited later; dated sunset possible. No file moves in this proposal beyond planning.

## Capabilities

### New Capabilities

- `docs-url-migration`: canonical versioned URL publication, compat mirror/redirect retention, and template-link cutover ordering.
- `agents-source-switch`: explicit-ref source switch with filename-map lockstep, strip-header re-verification, manual re-ingest, and no-silent-deletion.

### Modified Capabilities

- None (no existing specs in documentation-common yet).

## Impact

- Affects python-project-common template URLs, raw links, workflow download sources, copier instruction refs, and agents-common distribution maps.
- Blocked on `generalize-publisher-tracks` acceptance and staged proof; requires Tier-1 + Tier-2 review and operator cutover approval.
- Acceptance is consumer-surface: Python/Rust rendered links with fragments, raw refs, workflow inputs, agents populate, rename detection, replay/rollback.
