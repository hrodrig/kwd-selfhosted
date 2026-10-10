# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Changed

- README aligned with the hrodrig selfhosted family (hero, TOC, pick-a-path sections, layout, community policies/standards, gghstats clones badge).

## [0.1.0] - 2026-10-10

### Added

- Bootstrap operator repository: Docker notes, Kubernetes manifests (CronJob + Deployment + RBAC), standalone linux/macos/bsd paths, and example YAML profiles.
- Docs gate: `make release-check` (VERSION, README badge, CHANGELOG) with CI on pull requests and pushes to `develop` / `main`.
- Default application image pin: `ghcr.io/hrodrig/kwd:v0.2.0`.

[Unreleased]: https://github.com/hrodrig/kwd-selfhosted/compare/v0.1.0...HEAD
[0.1.0]: https://github.com/hrodrig/kwd-selfhosted/releases/tag/v0.1.0
