# Changelog

All notable changes to this project are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.1.31]

**One pin moved: okf-skills `3fe5a48` (v0.1.12 → v0.1.13).**

- **okf-skills 0.1.13 widens what its guidance calls a summary.** A corpus audited on 2026-08-26
  carried **nineteen false or superseded summary claims** while its own conventions said *re-read the
  index* — **the rule was written, and it named one file of six.**

  `okf-bundle` had three observed failures on this and **all three were tallies**, so a reader would
  search for numbers; **most of the nineteen were not counts** but claims a concept had already
  corrected in its own body. It now names the six kinds of file that hold a summary, adds the
  diagnostic that nineteen of nineteen shared — *when a concept records it was wrong about something,
  search the corpus for the thing it was wrong about* — and records the two gates measured and
  refused, one of them at **249 candidate occurrences**.

  `okf-verify`'s release step named two files and now names six. `okf-concept` gains a subsection on
  the `description:` field, where **five of fifty** asserted what their own body denied.

- ⚠ **Checked before pinning, per the convention**: `3fe5a48863b78395e7bad84b4282aedaeb488ef7` is on
  `github` at both `refs/heads/main` and `refs/tags/v0.1.13^{}`. **A pin resolving to nothing installs
  nothing and the marketplace cannot report it.**

## [0.1.30]

**Two pins moved: okf-skills `cb43318` (v0.1.11 → v0.1.12) and structured-data-skills `a357df9`
(v0.1.6 → v0.1.7).**

- **okf-skills 0.1.12 restores the version lockstep.** 0.1.11 shipped with `metadata.version`
  `"0.1.10"` in all three `SKILL.md` files while `plugin.json` read `0.1.11`, so the `v0.1.11` tag
  records a plugin that contradicts itself about its own version. No skill content changed.
- **structured-data-skills 0.1.7 — *When the metadata lives in the prose*.** The case where a
  document has no separate metadata at all: an Architecture Decision Record keeps its number in the
  filename *and* the `# N.` heading, its status as a word in a section that also holds prose. `mq`
  addresses those by structure through its `section` module. The status case is measured — a trailing
  period parses as `Proposed`, and a hard wrap that puts `superseded` at the start of a line parses
  as `Superseded`, so **a line break changes a record's status and nothing reports it**. Also records
  that `to_text()` and `to_string()` are not interchangeable, which is how the rule was found.

## [0.1.29]

**okf-skills re-pinned to `7b7d871` (v0.1.10 → v0.1.11).**

Adds four faults found by a verification pass over six OKF bundles, none of which the skills already
covered:

- **Mistrims run in one direction** — every mistrimmed quotation in that corpus ended where the
  surrounding *argument* wanted the sentence to end, which makes it the argument leaking into the
  evidence rather than transcription noise, and explains why re-reading never catches it.
- **A figure from a page that recomputes should not be quoted** — one statistics page recalculated
  weekly *and* rendered amounts in the viewer's currency, giving two different numbers for the same
  period. Report with a read-on date instead.
- **Three concept anti-patterns** — a number in prose that a gate already counts, a verification note
  that outlives its evidence, and a comparison table captioned only at the foot of the page.
- **Bundles whose sources cannot be followed must say so in the index** — a corpus citing reserved
  documentation hosts is unverifiable by construction, which is invisible from inside it.

Notably *not* added: mechanical quotation checking, drafting from the downloaded source, and not
quoting your own claim in a re-verification note. All three were already in the skills, with better
evidence than the pass produced.


## [0.1.28]

### Changed

- Refreshed `structured-data-skills` to `66e90cd` (v0.1.6): **choose the artifact before the tool.**
  `process-structured-data` gains *A rendered document is not the document* — when something is
  published in several formats, one is usually canonical and the rest are renderings, and parsing a
  rendering means reverse-engineering layout that was never content. IETF RFCs are the worked case,
  with the exact boundary (RFC 8650 is the first with `.xml`) probed rather than recalled.
  - The transferable half: **check status before you quote.** A verbatim quotation from a superseded
    document passes every string check, because the text really does say that — `rfc-index.xml`
    reports RFC 2616 as obsoleted by RFC7230..RFC7235. Any corpus of citations wants a status check
    beside its text check.
  - `extract-document-text` gains a four-rung fetch ladder ending in Playwright, for content that
    does not exist until JavaScript runs — with the rule that a browser produces evidence needing its
    version recorded.

## [0.1.27]

### Changed

- Refreshed `structured-data-skills` to `cc0f456` (v0.1.5): **`extract-document-text` documented one
  of xberg's two distributions without saying which.** It described the Python package's async API;
  a reader who installed `xberg-cli`, the Rust binary, found none of it applicable and nothing
  explaining why. The skill now names the split and covers both.
  - **The finding is one the CLI's own help does not make**: `xberg extract --stdin` without `-m`
    emits the raw file bytes and exits 0 — `%PDF-1.3 … stream`, the container instead of the
    document, reported as success. MIME detection works from a path and not from a pipe, so the hint
    is load-bearing there. Surfaced by running every documented command rather than transcribing it.
  - Guidance applying to both distributions — `extraction_method`, structure recovery, the OCR engine
    note, the not-quotable warning — moved out from under the Python example where it had been
    silently scoped to one.
- **First re-pin under the `pin-recorded` gate**, which now fails a commit that moves a SHA without
  moving this `version` and citing the new pin here.

## [0.1.26]

### Changed

- Refreshed `project-orchestration-skills` to `0a1301d` (v0.1.34), five releases on from the
  pinned v0.1.29. **The pin, not the plugin, was the stale part** — a marketplace `autoUpdate`
  refreshes this repository and never the SHAs inside it, so a plugin can sit five releases
  behind while every clone reports itself up to date.
  - **v0.1.33 — an agent signed a DCO attestation in a maintainer's name.** A `commit-msg` hook
    rejected a commit for a missing `Signed-off-by:`, and `git commit -s` satisfied the hook by
    asserting a legal certification the agent had no standing to make. `setup-git-hooks` now says
    to hand the work back unsigned, and `bootstrap-project`'s generated `CLAUDE.md` carries
    *Attestations are never delegated* — generalised past the DCO to a CLA, a release approval,
    a published provenance statement. Ships as an instruction and says so: the hook still cannot
    tell a person from a tool.
  - **v0.1.34 — a repository with three remotes ran its pre-push gates on two of them and
    reported a clean summary for the third.** lefthook derives the pre-push file set from
    `@{push}`, which git resolves per *branch*, so the first push advances it and every later
    remote computes an empty diff. `pre-push` gates belong in `scripts:`, which are not subject
    to the skip. Two non-fixes are recorded so they are not retried.
  - **v0.1.31–v0.1.32 — commit-message, README and code-comment content conventions**, shipped
    house-derived and then checked against Ousterhout's published exchange with Martin, which
    contradicted three of them. Interface comments were a missing category, not a refinement.
  - **v0.1.30** — `analyze-project` cites the `ai-contribution-policies` bundle and flags the
    `Co-developed-by:` trap.

### Notes

- `okf-skills` was re-pinned to `4d6d8f5` (v0.1.10) in `c575062` **without a changelog entry or
  a marketplace version bump**, as was the `structured-data-skills` v0.1.4 pin in `a0fa62e`.
  Both are recorded here rather than left out of the log: a pin change nobody can see in the
  changelog is a pin change nobody can audit.

## [0.1.25]

### Changed

- Refreshed `okf-skills` to `f585b26` (v0.1.9): **`okf-verify` gains a mechanical quotation check.**
  A quotation is the only part of a concept that cannot be judged by reading it — a stale claim looks
  stale, a misquotation looks perfect forever.
  - The useful half is the **normalisation that must precede the check**: page furniture, hyphenation
    across a line break, blockquote markers and emphasis inside the quoted span all produce *false
    negatives*, while rendered-versus-raw link text is a *real fault*. Treating one as the other
    corrupts a correct quotation.
  - Plus the trap specific to re-verification: a note about a claim you just revised invites quoting
    your own wording into the styling that means *the source wrote this*.

Marketplace `version` 0.1.24 → 0.1.25.

## [0.1.24]

### Changed

- Refreshed `okf-skills` to `7ffe590` (v0.1.8): **one rule, from four instances of the same failure
  in a single week.** `okf-bundle` now states that no gate compares an `index.md`'s claims to the
  corpus it indexes — an index that only links onward cannot drift, but one that characterises the
  collection holds a second copy of facts living in the concept files.
  - The instance worth the section: correcting a count to a *named exception* is the right instinct,
    and *"every concept but one is verified"* was still wrong on arrival, because the commit that
    wrote it added the second unverified file. **A named exception is robust against later change
    and not against the change introducing it.**
  - The guidance is to **describe the kind of evidence rather than quantify it** — a distribution
    stays true when a concept is added; a tally does not.
  - `okf-verify` gains a matching step: re-read `index.md` and any `landscape.md` before tagging,
    because a verification pass edits concepts and the index is not what you are editing.

Marketplace `version` 0.1.23 → 0.1.24.

## [0.1.23]

### Changed

- Refreshed `okf-skills` to `e123b80` (v0.1.7): **two gaps filled that were absent rather than
  wrong**, found by auditing three bundles built in one week against what the skills already said.
  - `okf-bundle` gains the **type vocabulary**, which it had not mentioned at all. OKF requires
    `type` and constrains no value — `type: Bananas` passes `okf validate` and `okf lint` with zero
    findings, run against a throwaway bundle and confirmed live by removing the field, which fails.
    The section is about checking the vocabulary in **both directions**, including the case a
    one-directional check cannot see: a type stranded when its only concept moves to another bundle.
  - `okf-verify` gains the outcome **between verified and unchecked** — a source that loads, is the
    right document, and does not support the claim. Absent `verified` conflates *never checked* with
    *checked and unsupported*, and only the second tells the next reader not to repeat the lookup.
  - Carries the heuristic behind it: **project documentation describes purpose, not failure modes**,
    so a tool's own page is nearly silent on what goes wrong with it.
- **The marketplace description named four subjects while six plugins shipped.** `okf-skills` and
  `structured-data-skills` had been added without it being updated, so the public listing understated
  what is here. Both are now named.

### Added

- Community health files: `SECURITY.md`, `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, `LICENSE` (MIT).

Marketplace `version` 0.1.22 → 0.1.23.

## [0.1.22]

### Changed

- Refreshed `c4-skills` to `dd47755` (v0.1.8), `diataxis-skills` to `e1e15d8` (v0.1.5) and
  `obsidian-skills` to `b2ba28c` (v0.1.6): all three **adopt `lefthook` for committed, reproducible
  git hooks**. The `gitleaks` gate previously lived only in `.git/hooks/pre-commit`, which git does
  not track — it did not survive a fresh clone, on repos whose purpose includes keeping homelab
  details out of public GitHub. `lefthook.yml` is committed, so `lefthook install` reproduces the
  gates anywhere. Each also gains `claude plugin validate`, verified complementary to the meta-repo's
  consistency gate with zero overlap. Both checks fail open when their tool is absent, so a missing
  local tool cannot block an external contribution.

  No skill content changed in any of the three — these are tooling-only releases.
  Marketplace `version` 0.1.21 → 0.1.22.

## [0.1.21]

### Changed

- Refreshed `project-orchestration-skills` to `9c61807` (v0.1.29): **`setup-pre-commit` renamed to
  `setup-git-hooks` — BREAKING**. Invoke the new name. The old one was wrong on two axes at once: it
  named one of the *two stages* the skill configures (pre-commit and pre-push, the latter carrying the
  expensive checks), and one of the *two hook managers* it already documents (`pre-commit` and
  `lefthook`) — while roughly half the skill, covering `.editorconfig`, secret-detection architecture,
  `.gitignore` hardening and multi-remote protection, involves no hook manager at all. The practical
  effect was that maintainers on Elixir, Go or Rust projects read "pre-commit", correctly inferred
  "that is the Python hook framework", and never reached the rest.

  **A deprecation stub remains at the old name until 0.2.0** — the skill, plugin and marketplace
  formats provide no rename, alias or redirect field, so content-level deprecation is the only
  graceful path the format offers. Splitting into `setup-pre-commit` + `setup-lefthook` was considered
  and rejected: it would duplicate ~340 lines of manager-neutral content. See workspace ADR-0013.
  Marketplace `version` 0.1.20 → 0.1.21.

## [0.1.20]

### Changed

- Refreshed `project-orchestration-skills` to `12e6c72` (v0.1.28): **workspace Sprint 2 — Inception &
  Establishment**. `analyze-project` now models what an upstream project requires **of a contributor**
  (DCO vs CLA, AI-contribution policy, inbound licence compatibility, governance) — a Phase 3 *Upstream
  Acceptance* subsection and a Phase 5 gap category, distinct from the dependencies you consume. Drawn
  from a real case where a contribution's acceptance criteria were discovered only after the code was
  written. (Sprint 2 also shipped a new **private** `workspace-skills` plugin via the incubator
  marketplace; it is not part of this public marketplace.) Marketplace `version` 0.1.19 → 0.1.20.

## [0.1.19]

### Changed

- Refreshed `project-orchestration-skills` to `51567c8` (v0.1.27): **workspace Sprint 1 — Release &
  CI-Publishing Integrity**. Five defects in the release/CI-publishing path, all found by *exercising*
  a real release (`ansible-bom`) rather than reading the skills, and each fix verified against the
  installed tool (cosign 3.1.1, syft 1.36.0) or vendor docs. `wrapup-sprint` now verifies every
  signature/attestation back in the release run as a gate (not just a consumer guide) and documents
  the cosign v3 bundle form; states release-job ordering so `slsa-github-generator` can't win the race
  and ship a bare notesless release; and requires the SBOM to catalogue the built **artifact** (not the
  source tree, which yields `pkg:github/*` and no stdlib) with a runnable CI subject assertion.
  `harden-github-actions` gains a private-repository control matrix (Scorecard/dependency-review/keyless
  signing self-activating at the public gate via `if: !repository.private`) and a note that Scorecard
  grades the default branch — which gitflow makes `develop`. Marketplace `version` 0.1.18 → 0.1.19.

## [0.1.18]

### Changed

- Refreshed `project-orchestration-skills` to `8312af7` (v0.1.26): toolchain floor vs build version
  becomes a quality gate. `setup-pre-commit`'s `quality-configuration.md` template now records three
  distinct roles — **Floor** (oldest runtime a consumer needs, from the language manifest), **Build**
  (what CI actually builds with), **Inherited** (a floor a dependency forces on you) — plus the
  per-call-site intent for every place CI selects a version. `validate-quality-config` gains a Step 6
  that asserts floor and build version *differ*; every other check in that skill asserts agreement,
  which is why this one was missing. Drawn from a real failure where lowering a Go floor silently
  moved every build onto it, shipping binaries built against a stdlib with two known advisories.
  Marketplace `version` 0.1.17 → 0.1.18.

## [0.1.16]

### Changed

- Refreshed `project-orchestration-skills` to `7e8c86b` (v0.1.25): `graduate-backlog` review-gate fixes. Most consequential: its `priority: *` label **colours** disagreed with the shared taxonomy, and each collided with a *different* label in it — and because label creation is idempotent-by-`|| true`, **first writer wins**, so the divergence would have been permanent and silent. Also fixed: Phase 5 created labels *after* the command that applies them (first run would fail); an eligibility clause still consulted the "Public" profile the skill had just decoupled from; `full` scope omitted the phase producing its headline output; and `roadmap-visible` was advertised but never implemented. Marketplace `version` 0.1.15 → 0.1.16.

## [0.1.15]

### Changed

- Refreshed `project-orchestration-skills` to `b7fa192` (v0.1.24): `harden-gitlab-ci` review-gate fixes. Most notably a **security gap** — the skill asserted `CI_JOB_TOKEN`'s own-project-only default without checking that it still holds; a project set to "All groups and projects" lets jobs from any project reach in, and has no allowlist to audit. Confirming the access mode is now the first step of that phase. The `audit` scope also gained tested detection commands (it had none, making it advisory rather than actionable). Marketplace `version` 0.1.14 → 0.1.15.

## [0.1.14]

### Changed

- Refreshed `project-orchestration-skills` to `b011194` (v0.1.23): adds **`harden-gitlab-ci`** (11 → 12 skills) — GitLab CI/CD supply-chain hardening (SHA-pinned `include:`/CI-Catalog components, `CI_JOB_TOKEN` allowlist scoping, masked+protected variables, `id_tokens`/OIDC, digest-pinned job images), for gitlab.com and self-hosted alike. A sibling of `harden-github-actions`, not a translation: GitLab's risks differ in kind. Also corrects a false claim in `harden-github-actions` that GitLab has no marketplace-action supply chain — GitLab's CI/CD Catalog needs the same SHA-pinning discipline. Marketplace `version` 0.1.13 → 0.1.14.

## [0.1.13]

### Changed

- Refreshed `project-orchestration-skills` to `dc13d10` (v0.1.22): **renames `harden-ci-workflows` → `harden-github-actions`**, owning the skill's GitHub coupling rather than hiding it inside a plugin that is otherwise forge-agnostic. Its controls are properties of the GitHub Actions execution model, not portable concepts in GitHub syntax; GitLab CI / Forgejo Actions are explicitly out of scope and tracked separately. Marketplace `version` 0.1.12 → 0.1.13.
- **Breaking for consumers**: the invocation name changes to `/harden-github-actions`. The old name is not aliased — update scripts and docs that reference it.

## [0.1.12]

### Changed

- Refreshed `project-orchestration-skills` to `5cf6a1c` (v0.1.21): adds the **`graduate-backlog`** skill (10 → 11 skills), moved from the maintenance plugin and decoupled from the Public distribution profile — backlog graduation is triggered by team scale, not exposure, so it now serves internal/corporate projects on self-hosted GitLab/Forgejo (workspace ADR-0008). Marketplace `version` 0.1.11 → 0.1.12. Card description now mentions work organization.

## [0.1.11]

### Changed

- Refreshed the two plugins carrying the **OCI-compliant-first** pass — `project-orchestration-skills` `c0c34de` (v0.1.20: `setup-container-security` reframed to OCI-first; `setup-architecture-as-code` Structurizr `-severity` → `-s`) and `c4-skills` `dfb65aa` (v0.1.7: documented the `inspect` subcommand; normalised the severity flag). `diataxis-skills` and `obsidian-skills` unchanged. Marketplace `version` 0.1.10 → 0.1.11.

## [0.1.10]

### Changed

- Repinned all four plugins to their CHANGELOG-backfill HEADs so each pinned tree contains its own release history — `project-orchestration-skills` `740cfa9`, `c4-skills` `3920736`, `diataxis-skills` `2c6893e`, `obsidian-skills` `03218f8`. No plugin-version change (docs-only). Marketplace `version` 0.1.9 → 0.1.10.

## [0.1.9]

### Changed

- Portfolio-review quality pass: refreshed all four plugins to their reviewed releases — `project-orchestration-skills` `53c4d73` (v0.1.19), `c4-skills` `aeaa20c` (v0.1.6), `diataxis-skills` `5d95604` (v0.1.4), `obsidian-skills` `2d67ef0` (v0.1.5). Fixes across 26 skills: broken pattern links → absolute URLs, Structurizr `-workspace`→`-w` + mount-root, `mix deps.audit` for Elixir CVEs, Diátaxis accent, and portability polish. Marketplace `version` 0.1.8 → 0.1.9; also accented "Diátaxis" in the marketplace card.

## [0.1.8]

### Changed

- Refreshed `project-orchestration-skills` to `aac7c9f` (v0.1.18): G4 review polish — `wrapup-sprint` now references the boundary ADR by its real title ("Work-Organization Boundary"). Marketplace `version` 0.1.7 → 0.1.8.

## [0.1.7]

### Changed

- Refreshed `project-orchestration-skills` to `00253f9` (v0.1.17): G4 tracker-boundary single-source-of-truth in `wrapup-sprint` + `bootstrap-project` (roadmap-vs-public-tracker canonical status). Marketplace `version` 0.1.6 → 0.1.7.

## [0.1.6]

### Changed

- Refreshed `project-orchestration-skills` to `2098a76` (v0.1.16): README skill roster synced to the full 10 skills. Marketplace `version` 0.1.5 → 0.1.6.

## [0.1.5]

### Changed

- Refreshed `project-orchestration-skills` to `44b6e5a` (v0.1.15): pins the marketplace to the plugin's completed C1–C10 compliance backlog, which adds the `harden-ci-workflows` and `setup-container-security` skills (8 → 10 skills). Marketplace `version` 0.1.4 → 0.1.5.

---

Releases prior to this changelog are recorded in the repository's git history.
Run `git tag --sort=-creatordate` to list released versions and
`git log <previous-tag>..<tag>` to see what changed in each.

The current version is `0.1.17` (see `.claude-plugin/marketplace.json`).
