# AGENTS.md

This file provides guidance to coding agents when working with code in this repository.

## Repository purpose

This is Team-MaRo's [special `.github` repository](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file). GitHub uses files here as **org-wide defaults** for any of the owner's repos that don't define their own. There is no application code, no build, no tests, no lint — just community-health docs and reusable workflow/config files.

Edits propagate implicitly: changing `CODE_OF_CONDUCT.md` here changes the displayed CoC for every Team-MaRo repo lacking its own copy. Treat changes as cross-repo policy edits.

## Layout

Two distinct surfaces — do not confuse them:

- **Repo root** (`README.md`, `LICENSE.txt`, `CODE_OF_CONDUCT.md`, `CONTRIBUTING.md`, `SECURITY.md`, `SUPPORT.md`, `CODEOWNERS`, `FEATURE_OR_BUG.md`, `.editorconfig`) — community-health docs, served as defaults to other repos.
- **`.github/` subdirectory** — config/automation for *this* repo only (does NOT propagate as defaults):
  - `dependabot.yml` — github-actions ecosystem, PRs target `develop` branch
  - `labeler.yml` — rules for `actions/labeler`
  - `ISSUE_TEMPLATE/` — bug + feature forms, `config.yml` disables blank issues
  - `PULL_REQUEST_TEMPLATE/default.md` — currently empty
  - `workflows/` — see below

## Workflows

- `dependabot-automerge.yml` — auto-approves + enables auto-merge for Dependabot PRs, but only when `github.repository == 'Team-MaRo/.github'`. Hard-coded repo guard; if forking or renaming, update the conditional.
- `dependabot-validate.yml` — validates `dependabot.yml` on push/PR touching it, sticky-comments result.
- `greetings.yml` — first-interaction welcome on new issues/PRs.
- `label.yml` — runs `actions/labeler` on every PR.
- `stale.yml` — daily cron, only acts on issues/PRs labeled `awaiting-feedback` or `awaiting-answers`; exempts `awaiting-approval` and `work-in-progress`.

## Branching model (from CONTRIBUTING.md)

- `develop` is the integration branch for new features. `master` is release.
- Dependabot targets `develop` (per `dependabot.yml`), not `master`.
- Bug fixes branch off the oldest affected release line; features branch off `develop`.

## Conventions

- Conventional Commits (per README) — used for automated releases/changelog in consumer repos.
- SemVer for tags.
- `.editorconfig` is authoritative for whitespace/EOL.
