# Old-base to new-base URL map (scaffold 2026-10-11)

Checked-in reviewed exact mapping pattern per migration spec.
Restricted to approved HTTPS origins and paths. Per-entry frozen/follow
declaration required; follow never inferred from shared fragments.
Old origin baseline: cutover-approved docs-1.9 snapshot, frozen.

```toml
# old_base and new_base are the only authorized origin+path roots.
old_base = "https://emcd.github.io/python-project-common/stable/sphinx-html/common/"
# new_base is set once canonical docs-2 host is published (operator decision).
new_base = "TODO-canonical-docs-2-base/"

# Each entry pins source fragment, destination fragment, and semantics.
# semantics = "frozen" | "follow" (follow requires reviewed + operator-approved update).
[[entries]]
source = "conduct.html"
destination = "conduct.html"
source_fragment = ""
destination_fragment = ""
semantics = "frozen"

[[entries]]
source = "environment.html#git-commit-signatures"
destination = "environment.html#git-commit-signatures"
source_fragment = "git-commit-signatures"
destination_fragment = "git-commit-signatures"
semantics = "frozen"
```

Validation: verify both endpoint HTML IDs, every inventoried link, and
redirect chains; reject missing, ambiguous, and arbitrary host/scheme
retargets. Schema rules: reject path traversal in source/destination,
require source uniqueness (one entry per source URL+fragment), default
semantics frozen, and carry a track field linking each entry to its
track-config alias once the schema lands (keeps map + track-config atomic).
Backup and provenance required for any mutated published HTML.
