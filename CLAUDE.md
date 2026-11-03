# jrjsmrtn-skills

Personal Claude Code skills marketplace. Contains a single `marketplace.json` manifest that references all published skill plugins.

## Structure

```
.claude-plugin/
  marketplace.json     # Marketplace manifest listing all published plugins
README.md
```

## Adding a Plugin

Add an entry to `.claude-plugin/marketplace.json` under `plugins`:

```json
{
  "name": "<plugin-name>",
  "description": "<one-line description>",
  "source": {
    "source": "url",
    "url": "https://github.com/jrjsmrtn/<plugin-name>.git",
    "sha": "<latest commit sha>"
  },
  "homepage": "https://github.com/jrjsmrtn/<plugin-name>"
}
```

Update the `sha` field whenever the referenced plugin is updated — see the Release Workflow below.

## Release Workflow

A release happens in two stages: each plugin is released on its own, then this marketplace is
re-pinned to the new release commits. Both stages commit **directly on `main`** — there is no
branch or PR step. *(This section described a branch-and-PR flow until 2026-11-03; the last ten
commits here and in `project-orchestration-skills` had all gone straight to `main`.)*

### Stage 1 — Release a plugin

In the plugin repo (e.g. `~/Projects/Skills/c4-skills`), on `main`:

1. **Land the change** as its own conventional commit (`feat:`, `fix:`, `docs:` …), with an entry
   under `## [Unreleased]` in the plugin's `CHANGELOG.md`.
2. **Bump versions:** `version` in `.claude-plugin/plugin.json` *and* `metadata.version` in
   **every** `SKILL.md` — not only the touched ones; they stay in lockstep.
3. **Date the CHANGELOG:** add `## [0.1.N] - YYYY-MM-DD` under `## [Unreleased]`.
4. **Commit** as `chore(release): v0.1.N — <summary>`, using a HEREDOC; include the
   `Co-Authored-By` footer when pair-programmed.
5. **Tag, signed and annotated:** `git tag -s v0.1.N -m "v0.1.N — <summary>"`.
6. **Push `main` and the tag to both remotes**, then confirm each holds them:
   ```
   for r in origin github; do git push "$r" main v0.1.N; done
   git ls-remote github refs/heads/main 'refs/tags/v0.1.N^{}'
   ```

**Pre-commit hooks:** each plugin repo has its own `lefthook.yml` — read it rather than assuming
which gates run (`project-orchestration-skills` runs gitleaks, `plugin-validate` and
`version-lockstep`).

**If `origin` (the private git server) is unreachable** — push only to `github` and continue;
catch up `origin` later. Safe because Stage 2 pins what is on `github`, not `origin`. Batch fix-up:
```
for repo in $(jq -r '.plugins[].name' .claude-plugin/marketplace.json) jrjsmrtn-skills; do
  git -C ~/Projects/Skills/$repo push origin main --follow-tags
done
```

### Stage 2 — Re-pin the marketplace

Back in this repo, on `main`:

1. **Pin the release commit, as GitHub has it** — the commit the tag points to, not the tag object:
   ```
   git ls-remote https://github.com/jrjsmrtn/<plugin>.git 'refs/tags/v0.1.N^{}'
   ```
   It must also be on `refs/heads/main` there. A SHA that resolves to nothing on GitHub installs
   nothing, and the marketplace cannot report it. Never pin a local-only commit, such as a no-op
   merge made while reconciling a diverged `origin`.
2. **Update** that plugin's `source.sha` in `.claude-plugin/marketplace.json`.
3. **Bump** `version` in `marketplace.json` (patch bump on any SHA change).
4. **Add a CHANGELOG entry** — `## [0.1.N]` naming each moved pin by its short SHA and version
   move, and recording that it was checked on GitHub before pinning.
5. **Commit** as `chore(pin): <plugin> v<old> -> v<new>` and push to both remotes.

The `pin-recorded` pre-commit hook enforces steps 3–4: when a pin moves, it blocks the commit
unless `CHANGELOG.md` is staged, the manifest `version` moved, and the staged CHANGELOG cites
each new pin's first seven characters. A pin commit should therefore touch exactly two files.

### Downstream consumers

Once Stage 2 lands:
- **Claude Code** users running `/plugin install github:jrjsmrtn/jrjsmrtn-skills` resolve the new plugin SHAs on their next install.
- **Other agents** (Copilot CLI, Cursor, Codex, Gemini CLI, …) installed via `gh skill install jrjsmrtn/<plugin>` pick up changes via `gh skill update --all`.

Both paths benefit from a single Stage 2 — no separate publishing step needed.

### Versioning rules

- Plugin `version` (in `plugin.json`): patch bump for any user-visible change to skills, README, CLAUDE.md, or plugin.json metadata. Don't bump for purely internal changes that don't affect installs.
- Per-skill `metadata.version` (in `SKILL.md`): tracks the parent plugin's `version` exactly, in every skill. Bump in lockstep.
- Marketplace `version` (in `marketplace.json`): patch bump on any SHA refresh, even if only one plugin changed.
- All three stay on `0.1.x` until the first deliberate `0.2.0` decision.

### Sync rule

When `origin` (private git server) diverges from `github` (e.g. an old commit only on origin), reconcile *before* the next release. Always merge `github` first so `main` matches GitHub, then push to `origin`. Never put a local-only merge SHA into `marketplace.json`.

## Published Plugins

Which plugins this marketplace publishes, and at which commit, is `.claude-plugin/marketplace.json`
— not restated here, because a copy drifts: this section listed four plugins while the manifest
published six. `README.md` keeps a reader-facing table of plugins and their skills; when a pin
moves, check that table's skill list against the skills at the new SHA.

## Remotes

- origin: private git server
- github: https://github.com/jrjsmrtn/jrjsmrtn-skills
