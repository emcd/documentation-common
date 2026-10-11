## 1. Canonical publication (gated: proposal approval authorizes implementation; staged-output review authorizes cutover consideration)

- [ ] 1.1 Confirm publisher-generalize acceptance and staged versioned proof before cutover
- [ ] 1.2 Publish canonical versioned URLs with ADR 003 anchors and checked-in old-base→new-base fragment mapping
- [ ] 1.3 Test endpoint HTML IDs, every versioned legacy-inventory entry, and redirect chains; reject unapproved retargets

## 2. Compatibility

- [ ] 2.1 Retain and verify compat mirror/redirects at old stable paths plus every legacy-inventory entry and fragment on each milestone, with endpoint probing and manifest comparison blocking on drift
- [ ] 2.2 Sweep known release matrices with provenance and backups, pinning the frozen docs-1.9 baseline and recording any explicitly authorized compat-track follow; name owner and validation job
- [ ] 2.3 Test frozen-versus-follow declaration and backup and provenance retention for mutated HTML

## 3. Consumer cutover (gated: no file moves until Tier-1/Tier-2 review + operator approval)

- [ ] 3.1 Update template assets to canonical URLs only after compat verification, keeping Rust generated-documentation links clean (no file moves until Tier-1/Tier-2 review + operator approval)
- [ ] 3.2 Execute atomic agents source switch at pinned commit with manifest, map lockstep, strip re-verification, manual re-ingest, rename detection, and rollback support (no file moves until Tier-1/Tier-2 review + operator approval)
- [ ] 3.3 Test failed fetch, map, and strip handling plus interrupted promotion and rollback
- [ ] 3.4 Obtain Tier-1/Tier-2 review and operator cutover approval before any file moves; revisit sunset date later
