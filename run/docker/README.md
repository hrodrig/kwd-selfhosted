# Docker — kwd

Run the published **distroless** image with a mounted kubeconfig and YAML profile.

**Image:** `ghcr.io/hrodrig/kwd:v0.2.0`

The image has **no shell**. Mount config and kubeconfig as files; pass args after the image name.

## One-shot (single-pass)

`interval: 0` in the profile (or override with `--interval 0`). Exit `0`/`1` like a cron job.

```bash
docker run --rm \
  -v "$HOME/.kube/config:/kube/config:ro" \
  -v "$(pwd)/run/examples/kwd-minimal.yml:/config/kwd.yml:ro" \
  -e KUBECONFIG=/kube/config \
  -e KWD_SLACK_WEBHOOK \
  ghcr.io/hrodrig/kwd:v0.2.0 \
  check --config /config/kwd.yml
```

Omit `KWD_SLACK_WEBHOOK` when the profile has no notification sinks, or set `dry_run: true`.

## Daemon (interval > 0)

Use a profile with `interval > 0` (see [kwd-daemon.yml](../examples/kwd-daemon.yml)). Publish the HTTP port only if `http.listen` is set and you scrape `/healthz` / `/metrics`.

```bash
docker run -d --name kwd \
  -v "$HOME/.kube/config:/kube/config:ro" \
  -v "$(pwd)/run/examples/kwd-daemon.yml:/config/kwd.yml:ro" \
  -e KUBECONFIG=/kube/config \
  -e KWD_SLACK_WEBHOOK \
  -p 127.0.0.1:8080:8080 \
  ghcr.io/hrodrig/kwd:v0.2.0 \
  check --config /config/kwd.yml
```

Prefer binding HTTP to loopback in the profile (`127.0.0.1:8080`); map host ports carefully.

**Stop:** `docker stop kwd && docker rm kwd`

## Notes

- In-cluster: prefer [kubernetes/manifests/](../kubernetes/manifests/) (ServiceAccount + RBAC) instead of mounting a user kubeconfig.
- Schema and flags: upstream [SPECIFICATIONS.md](https://github.com/hrodrig/kwd/blob/main/SPECIFICATIONS.md).
