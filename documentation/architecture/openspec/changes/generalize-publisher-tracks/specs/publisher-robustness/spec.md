## ADDED Requirements

### Requirement: Validated tree before promotion

The publisher SHALL build the full site tree and validate it via static-site-builder dry run, link checking, track-config and matrix schema validation, and immutable-tree presence before promoting aliases. Validation covers navigation, release matrices/indexes, immutable historical trees, and the versioned legacy-link inventory (seeded with 36 entries; all entries at the reviewed publication revision MUST validate, with explicit additions and removals).

#### Scenario: Staged versioned proof validates

- **WHEN** staged output for a versioned alias is built
- **THEN** old-input→old-output equivalence holds for package tracks and every legacy-link inventory entry resolves before promotion is allowed

#### Scenario: Drift blocks promotion

- **WHEN** public-endpoint probing or version and commit manifest comparison shows drift or absence
- **THEN** promotion is blocked and the previous good tree is retained

### Requirement: Serialized concurrent publications

Concurrent publications SHALL be serialized via destination-scoped CI concurrency plus remote-branch compare-and-swap or non-force push, and rebuild and replay from retained inputs SHALL be supported. The publisher SHALL fetch and read current publication state only after acquiring writer ownership; if the destination ref advances before commit or push, it SHALL refetch, rebuild, and revalidate or fail without lost updates. Concurrent CI cancellation SHALL NOT kill an active promotion. Deployment credentials SHALL appear only in the trusted publication job after staged validation, source commit and tool inputs SHALL be pinned, dangerous archives and symlinks SHALL be rejected during restore, and the last good output SHALL be retained on all failed inputs.

#### Scenario: Concurrent publishes do not clobber index

- **WHEN** two publications run concurrently
- **THEN** the version index reflects both in serialized order with no lost entries

#### Scenario: Destination advance triggers rebuild or fail

- **WHEN** the destination ref advances after writer ownership is acquired but before push
- **THEN** the publisher refetches, rebuilds, and revalidates or fails without lost updates
