# Example profiles

Operator starters for **kwd**. Canonical schema: [configs/kwd.sample.yml](https://github.com/hrodrig/kwd/blob/main/configs/kwd.sample.yml) and [SPECIFICATIONS.md](https://github.com/hrodrig/kwd/blob/main/SPECIFICATIONS.md).

| File | Shape |
|------|--------|
| [kwd-minimal.yml](kwd-minimal.yml) | Single-pass (`interval: 0`) — cron / CronJob exit `0`/`1` |
| [kwd-daemon.yml](kwd-daemon.yml) | Daemon (`interval > 0`) + `http.listen` |

**Scheduled HEALTH CHECK digests:** same profile as minimal + CLI `--force-notification` (see CronJob `kwd-report` under [../kubernetes/manifests/cronjob.yaml](../kubernetes/manifests/cronjob.yaml) and linux cron examples). Smoke sinks: `kwd notify test --config …`.

Edit `resources:` to match your cluster. Do not commit real webhook URLs — use `KWD_SLACK_WEBHOOK` in the environment or a Kubernetes Secret.
