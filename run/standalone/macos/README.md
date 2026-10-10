# macOS (standalone binary)

← [Back to run/standalone](../README.md).

1. Download a **darwin** tarball from **[kwd Releases](https://github.com/hrodrig/kwd/releases)** (`amd64` or `arm64`).
2. Extract **`kwd`** onto your `PATH`.
3. Use a profile from [run/examples/](../../examples/README.md); point `KUBECONFIG` at your kubeconfig.

**One-shot / cron:** `crontab -e` with `kwd check --config …` and `interval: 0`.

**Daemon:** run under `launchd` or a terminal multiplexer with `interval > 0`. Homebrew tap for **kwd** is not published yet — use the release binary or `go install github.com/hrodrig/kwd@v0.2.0`.
