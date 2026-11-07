# Kubernetes — kwd

Flat manifests under **[manifests/](manifests/)**. No Helm chart in v0.1.x.

**Image pin:** `ghcr.io/hrodrig/kwd:v0.4.0`

## Apply order

```bash
kubectl apply -f manifests/namespace.yaml
kubectl apply -f manifests/rbac.yaml
kubectl apply -f manifests/configmap.yaml
# Create Secret from secret.example.yaml (edit webhook first) — do not commit real values
# kubectl apply -f manifests/secret.yaml   # after copying from secret.example.yaml
```

Then choose shapes:

| Shape | Manifest | Profile |
|-------|----------|---------|
| Scheduled readiness gate | [manifests/cronjob.yaml](manifests/cronjob.yaml) `kwd-check` | `interval: 0` — exit `0`/`1`; Slack only when not ready |
| Scheduled HEALTH CHECK digest | same file, CronJob `kwd-report` | `--force-notification` — always FanOut (healthy → green digest) |
| Long-running daemon | [manifests/deployment.yaml](manifests/deployment.yaml) (+ Service) | `interval > 0` + `http.listen` |

Edit ConfigMap data to match your resources. RBAC is **read-only** (`get`/`list`/`watch` on deployments and statefulsets).

### Validate infra from a CronJob

1. List real refs under `resources:` in ConfigMap `kwd.yml`.
2. Apply Secret `kwd-notify` with `KWD_SLACK_WEBHOOK` (Slack or Discord Incoming Webhook URL).
3. Apply both CronJobs (or delete `kwd-report` if you only want exit-code gates).
4. Smoke sinks without a cluster check: run a one-shot Job with `args: ["notify", "test", "--config", "/config/kwd.yml"]`.
5. Force a digest now:

```bash
kubectl create job --from=cronjob/kwd-report kwd-report-manual -n kwd
kubectl logs -n kwd job/kwd-report-manual -f
```

Healthy digests look like: `✅ Success` + `HEALTH CHECK: All resources ready` + Cluster / Client / Time / Namespace / Status / Action Required + Details.

## Secrets

Copy [manifests/secret.example.yaml](manifests/secret.example.yaml), set `KWD_SLACK_WEBHOOK`, apply as `kwd-notify` in namespace `kwd`. Omit the Secret and notification sinks if you do not use Slack.

## Daemon HTTP / CVE-2026-98432

Deployment sets `GODEBUG=multipathtcp=0`. Upstream **kwd** also disables MPTCP on the listen socket. **Primary fix:** patched Linux kernel on nodes. Prefer loopback `http.listen` only when scrapers can reach it (in-cluster Service probes usually need `0.0.0.0`). See [golang-announce](https://groups.google.com/g/golang-announce/c/PCoQcdxoScw) and [CVE-2026-98432](https://nvd.nist.gov/vuln/detail/CVE-2026-98432).
