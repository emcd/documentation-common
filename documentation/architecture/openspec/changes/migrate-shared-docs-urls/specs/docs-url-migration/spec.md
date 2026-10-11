## ADDED Requirements

### Requirement: Canonical docs-2 URLs with compat retention

The system SHALL publish canonical docs-2 URLs in documentation-common while retaining a compat mirror or redirects at old python-project-common `stable/sphinx-html/common/` paths, with template asset updates occurring only after compat is verified. Compatibility-contract ownership SHALL rest with Documentation Owner and old-origin deployment ownership with the Python site owner, both using the same reviewed and pinned pipeline. The rewrite mapping SHALL be a checked-in reviewed exact mapping restricted to approved HTTPS origins and paths with source-to-destination fragment IDs. Old URLs and fragments SHALL persist until explicit operator retirement.

#### Scenario: New consumers use canonical URLs

- **WHEN** a new project renders after cutover
- **THEN** its links target the canonical docs-2 URLs with ADR 003 anchors intact

#### Scenario: Old baked links keep resolving

- **WHEN** an already-rendered README with old stable links is fetched
- **THEN** those links resolve via the compat mirror or redirects with fragments verified

#### Scenario: Invalid mapping rejected

- **WHEN** a mapping entry is missing, ambiguous, or targets an unapproved host or scheme
- **THEN** the change is rejected and no published HTML is mutated

### Requirement: Frozen baseline semantics for old origin

Old-origin pages SHALL retain the cutover-approved docs-1.9 compatibility snapshot, unchanged, until an explicitly reviewed and operator-approved compatibility-track update. New consumers SHALL use docs-2. Per-entry mappings MAY declare frozen or follow, but following another docs-major SHALL never be inferred merely because the destination shares the same fragment identifier. If the snapshot docs-1.9 is not the currently served content, the actual reviewed cutover snapshot SHALL be selected and recorded rather than blindly replacing existing semantics.

#### Scenario: Old origin serves frozen baseline

- **WHEN** an old stable URL is requested after cutover without an authorized compat-track update
- **THEN** it serves the pinned docs-1.9 compatibility snapshot content unchanged

#### Scenario: Follow requires explicit authorization

- **WHEN** a per-entry mapping proposes following a newer docs-major
- **THEN** it is rejected unless an explicitly reviewed and operator-approved compat-track update authorizes it
