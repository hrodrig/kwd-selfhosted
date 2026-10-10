# run/ — operator deployment index

This tree holds **how to run kwd**, not the CLI source. Product docs: [kwd](https://github.com/hrodrig/kwd).

**Image pin (default in manifests):** `ghcr.io/hrodrig/kwd:v0.2.0`

| Directory | Purpose |
|-----------|---------|
| [docker/](docker/README.md) | Run the published image on a bastion with kubeconfig + config mount |
| [kubernetes/](kubernetes/README.md) | In-cluster CronJob (single-pass) or Deployment (daemon) + RBAC |
| [standalone/](standalone/README.md) | **cron** and **systemd** using the Releases binary |
| [examples/](examples/README.md) | Minimal operator profiles |

## Pick a path

| You have… | Start here |
|-----------|------------|
| kubeconfig on a laptop / bastion | [docker/README.md](docker/README.md) |
| Kubernetes, scheduled single-pass | [kubernetes/manifests/cronjob.yaml](kubernetes/manifests/cronjob.yaml) |
| Kubernetes, long-running daemon | [kubernetes/manifests/deployment.yaml](kubernetes/manifests/deployment.yaml) |
| Linux host + cron only | [standalone/README.md](standalone/README.md) |
| Need a starter config | [examples/](examples/README.md) |

## Related upstream docs

- [SPECIFICATIONS.md](https://github.com/hrodrig/kwd/blob/main/SPECIFICATIONS.md) — behavior contract
- [configs/kwd.sample.yml](https://github.com/hrodrig/kwd/blob/main/configs/kwd.sample.yml) — all config keys
- [kwd README — Install](https://github.com/hrodrig/kwd/blob/main/README.md#install) — deb, rpm, tarball, `go install`
