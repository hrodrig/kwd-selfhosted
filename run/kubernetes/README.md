# Kubernetes — kwd

Flat manifests under **[manifests/](manifests/)**. No Helm chart in v0.1.0.

**Image pin:** `ghcr.io/hrodrig/kwd:v0.2.0`

## Apply order

```bash
kubectl apply -f manifests/namespace.yaml
kubectl apply -f manifests/rbac.yaml
kubectl apply -f manifests/configmap.yaml
# Create Secret from secret.example.yaml (edit webhook first) — do not commit real values
# kubectl apply -f manifests/secret.yaml   # after copying from secret.example.yaml
```

Then choose **one** shape:

| Shape | Manifest | Profile |
|-------|----------|---------|
| Scheduled single-pass | [manifests/cronjob.yaml](manifests/cronjob.yaml) | `interval: 0` in ConfigMap |
| Long-running daemon | [manifests/deployment.yaml](manifests/deployment.yaml) (+ Service) | `interval > 0` + `http.listen` |

Edit ConfigMap data to match your resources. RBAC is **read-only** (`get`/`list`/`watch` on deployments and statefulsets).

## Secrets

Copy [manifests/secret.example.yaml](manifests/secret.example.yaml), set `KWD_SLACK_WEBHOOK`, apply as `kwd-notify` in namespace `kwd`. Omit the Secret and notification sinks if you do not use Slack.
