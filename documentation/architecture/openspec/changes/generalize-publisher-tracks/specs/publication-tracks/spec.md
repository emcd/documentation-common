## ADDED Requirements

### Requirement: Explicit publication tracks

The publisher SHALL support explicit tracks `stable`, `development`, and floating-major aliases (e.g. `v1/`), each matching its own tag namespace explicitly. Track configuration SHALL use kebab-case TOML keys and declare per track a tag namespace, selector, and alias, and SHALL be validated to reject path traversal and namespace collision. Floating majors SHALL resolve over finals only, never prereleases.

#### Scenario: Floating major publishes versioned alias

- **WHEN** releases in the `v1.*` line publish
- **THEN** a `v1/` subtree tracks the newest final `v1.*` release alongside `stable/` and `development/` without altering package-version alias selection

#### Scenario: Legacy stable behavior pinned

- **WHEN** package versions publish
- **THEN** `stable/` resolves to the newest final release and `development/` to the newest prerelease exactly as before

#### Scenario: Invalid track config rejected

- **WHEN** track configuration contains path traversal or namespaces colliding across tracks
- **THEN** publication fails without promoting any output

### Requirement: Atomic alias promotion

Alias promotion SHALL construct a complete validated tree before changing aliases and SHALL retain the previous good output when the source fails. Atomicity is one complete publication snapshot or branch update, not separate per-alias directory swaps.

#### Scenario: Failed source keeps previous tree

- **WHEN** a publication source fails validation
- **THEN** aliases continue to serve the previous good tree and no partial tree is promoted
