# Standalone — kwd binary

Run **kwd** from a [release tarball](https://github.com/hrodrig/kwd/releases) (or `go install` / package) without Docker.

| Platform | Notes |
|----------|--------|
| [linux/](linux/README.md) | cron one-shot + systemd daemon sketch |
| [macos/](macos/README.md) | launchd / cron notes |
| [bsd/](bsd/README.md) | FreeBSD / OpenBSD port skeletons in upstream **kwd** |

**Shapes:**

- **Single-pass:** `interval: 0` (or `KWD_INTERVAL=0`) — suitable for cron; exit `0`/`1`.
- **Daemon:** `interval > 0` — long-lived process; optional `http.listen` for `/healthz` and `/metrics`.

Starter configs: [../examples/](../examples/README.md).
