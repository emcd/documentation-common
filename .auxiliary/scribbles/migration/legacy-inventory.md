# Versioned legacy-link inventory (seeded 2026-10-11)

Source: `python-project-common` template + documentation stable links to
`https://emcd.github.io/python-project-common/stable/sphinx-html/common/`.
Seeded with 23 unique URLs (36 total occurrences per handbook/5).
All entries at reviewed publication revision MUST validate, with explicit
additions and removals. Frozen baseline: old origin retains the
cutover-approved docs-1.9 compatibility snapshot unchanged.

## Entries

- architecture-python.html
- architecture.html
- conduct.html
- environment-python.html
- environment.html
- environment.html#git-commit-signatures
- maintenance.html
- nomenclature-germanic.html
- nomenclature-latin.html
- nomenclature.html
- practices-python.html
- practices-rust.html
- practices-toml.html
- practices.html
- python-autoformat.html
- releases-python.html
- releases.html
- requirements.html
- style.html
- tests-python.html
- tests.html
- validation-python.html
- validation.html

## Provenance

- Inventoried from template/documentation stable references 2026-10-11.
- Reviewed revision pinned: docs-1.9 = 82082295a30c9ef2aa4c633bc609df70c4a0e127.
- Total occurrences: 36 (template README 1, contribution 33, prd 1, decisions index 1).
- Inventory versioning: each revision carries version and date; additions and removals are explicit at the reviewed revision.
- TOML contract (locked by Python Owner 2026-10-11, enforced by validator): `complete` optional (true requires every website file covered); per entry `path` relative only (no absolute/traversal), `sha256` required when semantics frozen and enforced whenever present, `fragments` optional list of parsed element IDs (strings rejected, no char-splitting, never substring), `semantics` frozen or follow. Inventory mandatory whenever resolved selections include docs-line aliases; package-only publishes stay inventory-optional.
- Advisor integration note 2026-10-11: keep reviewed legacy URL/fragment inventory SEPARATE from baseline retained-history manifest derived from the previously trusted snapshot. History completeness covers every retained HISTORICAL file with unchanged digests, excluding new version files and mutable aliases/index/provenance by class rules; compare candidate hashes to pre-build baseline (never regenerate blessings from candidate). For docs/compat publishing both checks mandatory; trigger from configured docs/compat track policy, not alias presence alone. Default complete=false alone cannot satisfy the guarantee.
- Owner: Documentation Owner (central inventory); site owners authorize per-site rewrites.
