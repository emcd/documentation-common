## Context

Canonical docs live in python-project-common today; documentation-common is nearly empty. Consumers: Python/Rust Copier templates bake `stable/sphinx-html/common/` HTTPS links at render time (36 links, 33 in contribution jinja); agents-common populates from `distribution/.../instructions/` (18 files, docs-1.9 pin) via pre-staged copy; workflows and raw links reference the same stable paths. Old git tags preserve source refs only, not hosted HTTP URLs. Operator signoff: no Copier/PyPI here, `emcdproj` stays, (b) first, sweep + mirror, two proposals. This change is gated on `generalize-publisher-tracks` staged proof.

## Goals / Non-Goals

**Goals:**
- Canonical docs-2 URLs published in documentation-common with ADR 003 anchors held.
- Compat mirror/redirects at old python paths retained beyond known-sites sweep; sweep reduces dependence, never proves deletability.
- Template updates only after compat verified; agents source switch atomic with URL change (explicit ref, file-map lockstep, strip re-verified, manual re-ingest, no silent deletion).
- Sunset revisited later (dated sunset possible); owner + validation job named.

**Non-Goals:**
- No publisher implementation (gated predecessor); no Rust rewrite; no deletion of common docs from python-project-common in this change.
- No sunset-date decision (revisit); no canonical-host move beyond URL publication.

## Decisions

- **Gate on publisher proof:** no URL cutover until generalized publisher is accepted with staged equivalence. Proposal approval authorizes implementation; staged-output review authorizes cutover consideration. Alternative (parallel cutover) rejected by validation-before-cutover invariant.
- **Mirror plus sweep, not sweep alone:** retain redirects/frozen mirror for unenumerated clients (every render, bookmarks, copies, issues). Ownership: Documentation Owner owns the compatibility contract; Python site owner owns old-origin deployment; both use the same reviewed and pinned pipeline with no independently edited mirror. Old URLs and fragments persist until explicit operator retirement, validated on each publication and cutover milestone. Alternative (sweep then delete) rejected by both template owners as hard requirement.
- **Atomic agents switch:** transactional staged snapshot plus manifest (source commit, selected files, mapping, strip parameters, output digests); validation before whole-snapshot promotion; rollback to the previous complete snapshot including map, ref, and header settings. A mutable tag is a selector resolved once to an exact commit and recorded; source, map, and strip all use that identity. Required missing or renamed files refuse and preserve the previous distribution. Manual re-ingest owner and downstream populate and update ownership are explicit; no blanket deletion of consumer edits. Alternative (staged drift) rejected: silent no-ops and warn-and-continue degrade.
- **Explicit rewrite mapping:** checked-in reviewed exact mapping (TOML) restricted to approved old and new HTTPS origins and paths, with source-to-destination fragment IDs plus a semantic frozen-or-follow declaration decided in spec. Verify both endpoint HTML IDs, every inventoried link, and redirect chains; reject missing, ambiguous, and arbitrary host or scheme retargets. Never mutate source tags or silently reroute old docs-major guidance to latest. Backup and provenance for any changed published HTML; site owner approves their site's change. Alternative (silent retarget) rejected.

## Risks / Trade-offs

- [Unknown clients break if mirror lapses] → Retain mirror/redirects; sunset only by explicit operator decision with inventory.
- [Renames silently no-op in agents maps] → Deleted/renamed-guide detection with explicit migration; fail REQUIRED misses instead of warn-and-continue.
- [Fragment drift across docs-major] → ADR 003 held; rename/removal requires docs-major bump.

## Migration Plan

1. Publisher generalize accepted with staged docs-2 proof.
2. Publish canonical docs-2; verify compat mirror/redirects and every versioned legacy-inventory entry plus fragments.
3. Update template assets; execute atomic agents source switch with manual re-ingest.
4. Operator cutover approval; sunset revisited later (dated sunset possible).

## Open Questions

- None blocking; frozen baseline is pinned in spec (old origin retains cutover-approved docs-1.9 snapshot unchanged until explicitly reviewed and operator-approved update; new consumers use docs-2; per-entry follow never inferred), mapping construction is a checked-in TOML file, and the known-sites inventory is a versioned list seeded from template links with Docs Owner as central owner.
