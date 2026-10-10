# Agent Guidelines (kwd-selfhosted)

Context and instructions for AI coding agents working on **kwd-selfhosted** (operator docs and manifests for the **kwd** CLI). See [agents.md](https://agents.md/) for the format.

## Project overview

- **What it is:** Operator-focused **documentation and manifests** for running **[kwd](https://github.com/hrodrig/kwd)** on a bastion, via cron/systemd, Docker, or in-cluster CronJob/Deployment. **No Go application code** in this repository.
- **Upstream application:** **[hrodrig/kwd](https://github.com/hrodrig/kwd)** owns the CLI, **`make release-check`**, tests, packages, and **`ghcr.io/hrodrig/kwd`** images. Config contract: **[SPECIFICATIONS.md](https://github.com/hrodrig/kwd/blob/main/SPECIFICATIONS.md)**.
- **`.cursor/`** is **local-only** (not committed). Shared agent policy belongs in tracked files such as this **AGENTS.md**, **README**, and **CONTRIBUTING.md**.

## Scope (operator vs product)

| **kwd-selfhosted** | **[hrodrig/kwd](https://github.com/hrodrig/kwd)** |
|--------------------|-----------------------------------------------------|
| Operator README, **`run/`** | Go CLI, engine, **`make release-check`**, packages |
| Example YAML under **`run/examples/`** | Canonical sample: **`configs/kwd.sample.yml`** |
| In-cluster CronJob / Deployment + RBAC | Readiness checkers and daemon HTTP |

**Not here (yet):** Docker Compose, Helm chart. Prefer flat manifests under **`run/kubernetes/manifests/`**.

**Do not** invent YAML keys in examples that the application does not support — when upstream schema changes, update **`run/examples/*.yml`** and README snippets together.

## Two version names

| Name | Meaning |
|------|---------|
| Root **`VERSION`** + README badge + Git tag **`v*`** | Snapshot of **this** repo (docs/examples) |
| **`ghcr.io/hrodrig/kwd:vX.Y.Z`** in docs/manifests | **kwd** application image — pin published [kwd releases](https://github.com/hrodrig/kwd/releases) only |

Do **not** bump this repo’s `VERSION` only to mirror an app tag.

## Checks and make targets

- **`make release-check`** — VERSION semver, README **Version** badge, CHANGELOG section for current VERSION. Script: **`testing/scripts/release-check.sh`**.

**Application gate:** clone **kwd** and run **`make release-check`** there before tagging an upstream app release.

## Git flow

- **Branches:** Work on **`develop`**. Topic branch → **PR into `develop`**. Release snapshot: **PR `develop` → `main`**, then annotated tag **`v<semver>`** on **`main`**.
- **Never** merge to **`main`**, create/push a release tag, or trigger [**.github/workflows/release.yml**](.github/workflows/release.yml) **without explicit user approval**.
- **Commits:** Show the proposed commit message and wait for user approval before `git commit`.
- **Language:** English only for code, comments, commit messages, docs, and README.

## Version bump (this repo)

| # | Artifact | Action |
|---|----------|--------|
| 1 | **`VERSION`** | New semver without `v` |
| 2 | **`README.md`** | Static **Version** badge `version-<semver>` |
| 3 | **`CHANGELOG.md`** | Move `[Unreleased]` into `## [X.Y.Z] - YYYY-MM-DD` |
| 4 | **Upstream pins** | When documenting a new **kwd** app release: update **`ghcr.io/hrodrig/kwd:v…`** in **`run/`** |
| 5 | **Gate** | `make release-check` |
| 6 | **Ship** | Merge `develop` → `main`, annotated tag — **only after user approves** |

## Repository structure

- **`run/docker/`** — `docker run` notes (distroless image; mount kubeconfig + config).
- **`run/examples/`** — operator YAML samples; must match upstream SPEC.
- **`run/kubernetes/manifests/`** — CronJob (single-pass), Deployment (daemon), Service, RBAC.
- **`run/standalone/`** — binary + cron/systemd notes (linux, macos, bsd).
- **`testing/scripts/`** — `release-check.sh`, `extract-changelog.sh`.

## Pull request checklist

- Example YAML changes: validate against **[kwd SPECIFICATIONS](https://github.com/hrodrig/kwd/blob/main/SPECIFICATIONS.md)**.
- No real **kubeconfig** contents, tokens, or private cluster URLs in commits.
- Prefer published **`ghcr.io/hrodrig/kwd:v*`** pins — never `:latest` as the only documented default.

## Supply chain

Prefer reviewing manifests in this clone and image tags from documented upstreams (**GHCR** tags matching **kwd** releases). Avoid `curl | sh` unless the user explicitly accepts the risk.

## Other instructions

- **README:** Keep **Version** badge aligned with **`VERSION`**.
- **CHANGELOG:** Operator-facing changes under `[Unreleased]`; finalize on release.
- See **[CONTRIBUTING.md](CONTRIBUTING.md)** for published scope and release flow.
