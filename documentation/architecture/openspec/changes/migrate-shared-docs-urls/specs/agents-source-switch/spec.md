## ADDED Requirements

### Requirement: Atomic agents source switch

The agents source switch SHALL use a transactional staged snapshot plus manifest recording source commit, selected files, mapping, strip parameters, and output digests, with validation before whole-snapshot promotion and rollback to the previous complete snapshot including map, ref, and header settings. A mutable tag SHALL be resolved once to an exact commit and recorded; source, map, and strip SHALL all use that identity. The switch SHALL use an explicit pinned ref to documentation-common with filename-map lockstep, per-file strip-header re-verification, manual re-ingest into `distribution/.../instructions/`, and no silent deletion of previously populated files.

#### Scenario: Pinned re-ingest promotes cleanly

- **WHEN** documentation-common provides the staged files at the pinned ref
- **THEN** the file map names each file exactly, strip headers are re-verified per file, and the distribution snapshot promotes only after validation

#### Scenario: Required file miss fails the update

- **WHEN** a required guide, map entry, or ref fails to resolve
- **THEN** the update fails and the previous complete distribution is kept instead of warning and continuing

#### Scenario: Interrupted promotion rolls back

- **WHEN** promotion is interrupted after staging
- **THEN** the system rolls back to the previous complete snapshot with its map, ref, and header settings intact
