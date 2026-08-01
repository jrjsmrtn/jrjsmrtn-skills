# Contributing to jrjsmrtn-skills

This repository is a [Claude Code](https://claude.com/claude-code) plugin **marketplace**.
It contains no skills of its own — it aggregates the individual skill plugins via
`.claude-plugin/marketplace.json`, pinning each to a commit SHA.

## What Lives Here

- `.claude-plugin/marketplace.json` — the marketplace manifest (each plugin's name, source, and pinned `sha`).
- `README.md` — install instructions and the plugin catalog.

## Making Changes

1. Create a feature branch off `main`.
2. To add or update a plugin entry, edit `marketplace.json` **and** update the `README.md`
   catalog table to match — keep the two in sync.
3. Pin every plugin to an explicit commit `sha`, never a floating branch.
4. Bump `version` in `marketplace.json` following [Semantic Versioning](https://semver.org/)
   and add a `CHANGELOG.md` entry under `[Unreleased]`.

## Reporting Issues

Open an issue here for marketplace or installation problems. Report issues with an
individual plugin's behavior in **that plugin's own repository**.

## License

By contributing, you agree that your contributions are licensed under the [MIT License](LICENSE).
