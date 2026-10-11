## ADDED Requirements

### Requirement: Explicit publication tracks

The publisher SHALL support explicit tracks `stable`, `development`, and docs-line aliases (e.g. `docs-2/`), each matching its own tag namespace explicitly and never inferring docs selection from PEP 440 package tags. Track configuration SHALL declare per track a tag namespace, selector, and alias, and SHALL be validated to reject path traversal and namespace collision.

#### Scenario: Docs tag publishes docs-line alias

- **WHEN** a `docs-2` tag is published
- **THEN** a `docs-2/` subtree is produced alongside `stable/` and `development/` without altering package-version alias selection

#### Scenario: Legacy stable behavior pinned

- **WHEN** package versions publish with no docs tags present
- **THEN** `stable/` resolves to the newest final release and `development/` to the newest prerelease exactly as before

#### Scenario: Invalid track config rejected

- **WHEN** track configuration contains path traversal or a docs namespace colliding with package tags
- **THEN** publication fails without promoting any output

### Requirement: Atomic alias promotion

Alias promotion SHALL construct a complete validated tree before changing aliases and SHALL retain the previous good output when the source fails. Atomicity is one complete publication snapshot or branch update, not separate per-alias directory swaps.

#### Scenario: Failed source keeps previous tree

- **WHEN** a publication source fails validation
- **THEN** aliases continue to serve the previous good tree and no partial tree is promoted
