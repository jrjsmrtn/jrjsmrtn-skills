# Changelog

All notable changes to this project are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- Community health files: `SECURITY.md`, `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, `LICENSE` (MIT).

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
