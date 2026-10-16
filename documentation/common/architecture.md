<!--
  Licensed under the Apache License, Version 2.0 (the "License");
  you may not use this file except in compliance with the License.
  You may obtain a copy of the License at

      http://www.apache.org/licenses/LICENSE-2.0

  Unless required by applicable law or agreed to in writing, software
  distributed under the License is distributed on an "AS IS" BASIS,
  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
  See the License for the specific language governing permissions and
  limitations under the License.
-->

<a id="architecture-documentation"></a>
# Architecture Documentation

Architecture documentation lives close to the source modules it describes —
not in a centralized architecture directory. This guide states where each
kind of design knowledge goes so that humans and agents look in the same
places.

<a id="where-design-knowledge-goes"></a>
## Where Design Knowledge Goes

- **Subsystem README files** (`README.md` in the directory nearest the
  sources) carry stable subsystem architecture, design rationale, and local
  constraints. Start discovery at the repository root README, then read the
  nearest subtree README before broadening any search. When implementation
  structure or operational patterns change, update the affected README in
  the same batch rather than recreating centralized mirrors under
  `documentation/`.
- **OpenSpec specs and designs** carry accepted capability requirements and
  cross-cutting or architectural decisions. Manage new capabilities,
  breaking changes, and architectural shifts through OpenSpec changes and
  keep accepted specifications synchronized when changes complete.
- **Project notebooks** carry coordination, not design: handoffs, issues,
  and todos. Do not duplicate design rationale in notebook notes; link to
  the README or spec instead. A separate notebook designs category is an
  anti-pattern because it creates an extra place to look that goes stale.
- **Code comments** explain non-obvious behavior only. Long discursive
  design or architecture narrative belongs in design docs, specs, or
  subsystem READMEs — never in comments, and never as transient
  administrative metadata (todo IDs, ticket folklore, coordination state).

<a id="directives"></a>
## Directives

Directives are the architecture decision records of this ecosystem. They
are not maintained as standalone ADR documents; each directive lives with
the workflow or standard it governs:

- Agent behavior directives live in the agent configuration
  (entrypoint guidance, procedures, and review flow).
- Project-specific directives live in `@.auxiliary/agents/project.md`.
- Versioned workflow contracts (publication tracks, compatibility promises)
  live in OpenSpec specs, where SHALL/MUST wording makes them testable.

If standalone ADRs return, they will come through the Nbspec project —
not through a revived centralized architecture directory.
