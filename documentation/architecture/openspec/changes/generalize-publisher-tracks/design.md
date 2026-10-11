## Context

Current publisher lives in python-project-common (`sources/emcdproj/website.py:218-297`, rendered via `data/templates/website.html.jinja`). It publishes a concrete version directory on `emcdproj website update <version> --production`, then copies newest final → `stable/` and newest prerelease → `development/` using `packaging.Version` ordering. Four version tracks share the repo today (emcdproj pkg, Copier template, common docs, GHA workflows); Copier default was kept sane by forcing template versions above package versions. Stakeholders: Python Template Owner (publisher owner), Documentation Owner (consumer), Agents Owner (host-agnostic), Rust Owner (matrices preserved), Reviewer General + Advisor (validation-before-cutover invariant). Operator signoff: generalize-first (b), no Copier/PyPI in docs-common, `emcdproj` stays.

## Goals / Non-Goals

**Goals:**
- Tag-driven explicit tracks: `stable`, `development`, plus docs-line aliases (`docs-2/`, future `docs-3/`), each matching its own tag namespace explicitly.
- Regression-pinned legacy behavior: existing stable/dev selection unchanged for package versions until cutover is proven.
- Robust promotion: complete validated tree before alias changes; retain previous good output on source failure; serialize concurrent publications; replay/rollback supported.
- Matrices and history preserved: per-project release matrices/indexes, immutable historical trees, atomic alias promotion.

**Non-Goals:**
- No canonical-host move in this change; no Copier template; no PyPI package move; no Rust rewrite (third future proposal).
- No URL cutover or template-link updates (gated follow-up change).
- No compat-mirror sunset decision (revisited later; dated sunset possible).

## Decisions

- **Explicit track config over version inference:** each track declares its tag namespace and selector; docs tracks never derive from PEP 440 package ordering. Track-config schema (precondition, TOML): `[tracks.<name>]` with `tag_namespace` (e.g. `docs-*`, `v*`), `selector` (`latest-final`, `latest-prerelease`, `exact-tag`), and `alias` (`stable/`, `development/`, `docs-2/`). Config is validated to reject path traversal and namespace collision (docs tag != package tag). Alternative (coerce `docs-2` into `packaging.Version`) rejected: separate axis, breaks ordering.
- **Regression-pin then generalize:** keep current hatch-version path green while adding tag-driven path behind staged fixtures. Alternative (rewrite in place) rejected: higher breakage risk for live stable links.
- **Staged proof before authority switch:** validate docs-2 aliases/anchors in staged output against old-input→old-output equivalence. Alternative (cut over then fix) rejected by validation-before-cutover invariant.
- **Atomic promotion with retention:** atomicity is one complete publication snapshot/branch update (host deployment may be async), not per-alias directory swaps. Build full tree, validate, then promote; keep prior good tree on failure. Alternative (in-place mutation) rejected: risks partial publishes.
- **Serialization via destination-scoped CI concurrency plus remote compare-and-swap:** local flock alone cannot serialize independent runners or manual publishers. Fetch and read current publication state only after acquiring writer ownership; if the destination ref advances before commit/push, refetch, rebuild, and revalidate or fail without lost updates. Concurrent CI cancellation must not kill an active promotion; queue/lock semantics preserve each accepted publication. Add stale-index, two-writer, and failure-after-staging pins. Alternative (flock only) rejected per Tier-2.
- **Validated-tree criteria:** static-site-builder dry run plus link checker over navigation and the versioned legacy-link inventory, schema validation of track config and release matrices/indexes, and immutable-tree presence check. Alternative (eyeball diff) rejected: must block cutover on drift.
- **Credentials and provenance:** deployment credentials only in the trusted publication job after staged validation, never in PR-provided code or config running with write authority. Pin source commit and publisher/tool inputs; an HTTPS clone alone is not provenance. Record tag→commit once and use that identity throughout.

## Risks / Trade-offs

- [Concurrent publishes overwrite version index] → Destination-scoped CI concurrency plus compare-and-swap non-force push; fetch-after-ownership; refetch/rebuild/revalidate or fail; cancellation-safe queue; stale-index/two-writer/failure-after-staging pins.
- [Tag-namespace confusion (pkg vs docs vs template)] → Explicit per-track matching with validated schema; ban package-tag ordering for docs tracks; record provenance (tag→commit once).
- [Staged vs live divergence] → Compare staged output against live fixtures including the versioned legacy-link inventory (36 entries seeded) before promotion; probe public endpoints and compare version/commit manifests for drift; block on mismatch.
- [Traversal or collision via config] → Validate track config for path traversal and namespace collision; reject dangerous archives and symlinks during restore.

## Migration Plan

1. Proposal approval authorizes implementation of the generalized publisher in python-project-common with staged docs-2 proof, old behavior pinned.
2. Staged-output review (Tier-1 re-review plus validation-before-cutover check) authorizes cutover consideration.
3. URL/source migration change proceeds only after this change is accepted; extraction/rewrite follows later.

## Open Questions

- None blocking; lock, validation criteria, and schema are fixed above. Remaining detail (exact CI concurrency group names) is implementation detail.
