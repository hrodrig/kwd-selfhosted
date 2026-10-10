# Linux (standalone binary)

← [Back to run/standalone](../README.md) · [run/README](../../README.md).

1. Download a **Linux** tarball from **[kwd Releases](https://github.com/hrodrig/kwd/releases)** (e.g. `kwd_v0.2.0_linux_amd64.tar.gz`).
2. Extract **`kwd`** (and optionally **`kubectl-kwd`**), then `chmod +x kwd`.
3. Copy a profile (e.g. [kwd-minimal.yml](../../examples/kwd-minimal.yml)) and edit `resources:`.

## Cron / one-shot (no daemon)

```bash
export KUBECONFIG=/home/kwd/.kube/config
# optional: export KWD_SLACK_WEBHOOK=...
*/5 * * * * /usr/local/bin/kwd check --config /etc/kwd/kwd.yml >>/var/log/kwd.log 2>&1
```

Profile must use `interval: 0` (default in kwd-minimal.yml).

## systemd (daemon)

Use a profile with `interval > 0` ([kwd-daemon.yml](../../examples/kwd-daemon.yml)). Example unit sketch:

```ini
[Unit]
Description=kwd readiness watchdog
After=network-online.target

[Service]
Type=simple
User=kwd
Group=kwd
Environment=KUBECONFIG=/home/kwd/.kube/config
EnvironmentFile=-/etc/kwd/kwd.env
ExecStart=/usr/local/bin/kwd check --config /etc/kwd/kwd-daemon.yml
Restart=on-failure
RestartSec=10

[Install]
WantedBy=multi-user.target
```

Put `KWD_SLACK_WEBHOOK=...` in `/etc/kwd/kwd.env` (mode `0600`). Prefer `http.listen: 127.0.0.1:8080` unless scrapers need another bind.

Docker path: [run/docker/README.md](../../docker/README.md).
