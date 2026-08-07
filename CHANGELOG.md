# Changelog

All notable changes to **ias-agent-skills** are recorded here. Versions follow
[SemVer](https://semver.org). The version lives in `.claude-plugin/plugin.json`
and each release is tagged `vX.Y.Z` (cut with `scripts/release`).

## [Unreleased]

## [0.2.0]

- Add a pre-integration **Intake** step to all six `inappstory-*` skills: the
  agent now asks for the integration key on a first integration and clarifies
  underspecified requests (where the UI goes / which feature) before writing code.

## [0.1.0]

- Initial release: six `inappstory-*` skills (Android, iOS, Flutter, React
  Native, React, JS) — live docs router plus curated playbooks/pitfalls/decisions.
