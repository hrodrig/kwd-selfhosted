# kwd-selfhosted

[![Version](https://img.shields.io/badge/version-0.1.0-blue)](https://github.com/hrodrig/kwd-selfhosted/releases)
[![Release](https://img.shields.io/github/v/release/hrodrig/kwd-selfhosted?label=release)](https://github.com/hrodrig/kwd-selfhosted/releases)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)
[![App image on GHCR](https://img.shields.io/badge/image-ghcr.io%2Fhrodrig%2Fkwd-2496ED?logo=github)](https://github.com/hrodrig/kwd/pkgs/container/kwd)
[![kwd app](https://img.shields.io/badge/app-hrodrig%2Fkwd-181717?logo=github)](https://github.com/hrodrig/kwd)
[![CI](https://github.com/hrodrig/kwd-selfhosted/actions/workflows/ci.yml/badge.svg)](https://github.com/hrodrig/kwd-selfhosted/actions/workflows/ci.yml)

Operator assets for **[kwd](https://github.com/hrodrig/kwd)** — Docker, in-cluster manifests, and standalone cron/systemd notes. **This repository owns deployment-related work.** **[hrodrig/kwd](https://github.com/hrodrig/kwd)** is the application source, binaries, and container image only.

**Releases:** Root **`VERSION`** and Git tags **`v<semver>`** on **`main`** name repository snapshots. Prefer **`main`** or a **tag** for reproducible paths, not unreviewed **`develop`**.

**Default app image pin:** `ghcr.io/hrodrig/kwd:v0.2.0` ([kwd releases](https://github.com/hrodrig/kwd/releases)).

---

## Pick a path

| You have… | Start here |
|-----------|------------|
| kubeconfig on a laptop / bastion | [run/docker/README.md](run/docker/README.md) |
| Kubernetes, **scheduled** single-pass check | [run/kubernetes/manifests/cronjob.yaml](run/kubernetes/manifests/cronjob.yaml) |
| Kubernetes, **daemon** (`interval > 0`) + `/healthz` | [run/kubernetes/manifests/deployment.yaml](run/kubernetes/manifests/deployment.yaml) |
| Linux host + cron or systemd | [run/standalone/linux/README.md](run/standalone/linux/README.md) |
| Starter config | [run/examples/](run/examples/README.md) |

Deeper index: **[run/README.md](run/README.md)**.

---

## Versioning

| Field | Meaning |
|-------|---------|
| **`VERSION`** / tag **`v*`** | This repo (docs + manifests) |
| **`ghcr.io/hrodrig/kwd:vX.Y.Z`** | Upstream **kwd** application image |

Bump this repo’s **`VERSION`** when operator assets change. Pin a new app tag when documenting a new **kwd** release.

---

## Checks

```bash
make release-check
```

Application quality gate lives in **[hrodrig/kwd](https://github.com/hrodrig/kwd)** (`make release-check` there).

---

## Community and policies

- [CONTRIBUTING.md](CONTRIBUTING.md)
- [SECURITY.md](SECURITY.md)
- [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md)
- [AGENTS.md](AGENTS.md)
- [CHANGELOG.md](CHANGELOG.md)

## License

[MIT](./LICENSE)
