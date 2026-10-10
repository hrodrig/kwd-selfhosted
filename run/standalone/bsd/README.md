# FreeBSD / OpenBSD (standalone)

← [Back to run/standalone](../README.md).

Upstream **kwd** ships **port skeletons** (not yet in the official ports trees):

- FreeBSD: [contrib/freebsd/](https://github.com/hrodrig/kwd/tree/main/contrib/freebsd)
- OpenBSD: [contrib/openbsd/port/](https://github.com/hrodrig/kwd/tree/main/contrib/openbsd/port)

Or download **freebsd** / **openbsd** tarballs from **[kwd Releases](https://github.com/hrodrig/kwd/releases)** (e.g. `kwd_v0.2.0_freebsd_amd64.tar.gz`).

Operator shape is the same as Linux: cron + `interval: 0`, or a long-running process with `interval > 0`. Example profiles: [run/examples/](../../examples/README.md).
