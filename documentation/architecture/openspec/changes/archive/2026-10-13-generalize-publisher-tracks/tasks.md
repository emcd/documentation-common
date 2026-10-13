## 1. Track configuration

- [ ] 1.1 Define explicit per-track tag-namespace schema with kebab-case TOML keys, validated against traversal and collision
- [ ] 1.2 Add floating-major alias support (e.g. `v1/`) alongside stable/development with regression-pinned legacy selection
- [ ] 1.3 Test invalid track config rejection and namespace separation

## 2. Robust promotion

- [ ] 2.1 Build complete validated tree before alias changes (builder dry run, link check, schema validation, immutable-tree check, versioned legacy inventory), retaining previous good output on failure
- [ ] 2.2 Serialize concurrent publications via destination-scoped CI concurrency plus compare-and-swap, supporting rebuild/replay; pin inputs and reject dangerous archives/symlinks
- [ ] 2.3 Test concurrent publishes, destination-advance rebuild-or-fail, drift-blocked promotion, and failed-input retention

## 3. Staged proof and review (gated: proposal approval authorizes implementation; staged-output review authorizes cutover consideration; no cutover until Tier-1/Tier-2 review + operator approval)

- [ ] 3.1 Validate staged versioned output: old-input→old-output equivalence, matrices/indexes, immutable trees, every versioned legacy-inventory entry at the reviewed revision
- [ ] 3.2 Record tag→commit provenance once and obtain Tier-1 re-review plus validation-before-cutover check
