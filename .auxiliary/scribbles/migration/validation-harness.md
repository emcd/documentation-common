# Validation harness scaffolding (2026-10-11)

Scenario-linked test tasks per approved proposals. Local scaffolding only.

## Publisher (generalize-publisher-tracks)

- Invalid track config rejection + docs-versus-package namespace separation.
- Concurrent publishes + destination-advance rebuild-or-fail.
- Drift-blocked promotion (endpoint probing + manifest compare).
- Failed-input retention (last good tree kept).
- Old-input to old-output equivalence + versioned legacy inventory at reviewed revision.

## Migration (migrate-shared-docs-urls)

- Endpoint HTML IDs + every legacy-inventory entry + redirect chains; reject unapproved retargets.
- Frozen-versus-follow declaration + backup and provenance retention.
- Failed fetch, map, and strip handling + interrupted promotion and rollback.
- Shared-fragment inference negative pin: same fragment, different docs-major, no follow authorization → reject and preserve baseline.
