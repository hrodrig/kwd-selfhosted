# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Changed

- Default application image pin: `ghcr.io/hrodrig/kwd:v0.4.0` (was `v0.3.0`).
- Kubernetes: second CronJob `kwd-report` with `--force-notification` for scheduled HEALTH CHECK digests; `kwd-check` remains exit-code / alert-on-failure.
- Daemon Deployment sets `GODEBUG=multipathtcp=0` (CVE-2026-98432 belt-and-suspenders; primary fix is a patched kernel). Document in kubernetes / linux standalone notes (#9).

## [0.1.1] - 2026-11-02

### Changed

- Default application image pin: `ghcr.io/hrodrig/kwd:v0.3.0` (was `v0.2.0`).
- README: early-development (pre-1.0) disclaimer pointing at upstream kwd — not for sole production readiness/alerting until v1.0.0; use at your own risk.
- Standalone install examples pin `v0.3.0` tarballs / `go install` tag.

## [0.1.0] - 2026-10-10

### Added

- Bootstrap operator repository: Docker notes, Kubernetes manifests (CronJob + Deployment + RBAC), standalone linux/macos/bsd paths, and example YAML profiles.
- Docs gate: `make release-check` (VERSION, README badge, CHANGELOG) with CI on pull requests and pushes to `develop` / `main`.
- Default application image pin: `ghcr.io/hrodrig/kwd:v0.2.0`.
- README aligned with the hrodrig selfhosted family (hero, TOC, pick-a-path sections, layout, community policies/standards, gghstats clones badge).

[Unreleased]: https://github.com/hrodrig/kwd-selfhosted/compare/v0.1.1...HEAD
[0.1.1]: https://github.com/hrodrig/kwd-selfhosted/compare/v0.1.0...v0.1.1
[0.1.0]: https://github.com/hrodrig/kwd-selfhosted/releases/tag/v0.1.0
