# Deploy to Kubernetes + GitHub

Deploy the current changes to the jojo-homelab Kubernetes cluster and push to GitHub.

## Cluster facts (never re-discover these)

- **Minikube profile:** `jojo-homelab` (3-node cluster, `--kube-context jojo-homelab`)
- **Driver:** Docker — multi-node, so `minikube docker-env` does NOT work
- **Image loading:** Build locally with `docker build`, then `minikube image load -p jojo-homelab` into the cluster
- **Image pull policy:** `Never` (images must be present on nodes before helm upgrade)
- **Helm chart:** `./helm/gamilist` — namespace `gamilist`
- **Images:** `gamilist-backend:latest`, `gamilist-frontend:latest`
- **Git remote:** `github.com:jojo-homelab/gamilist.git`, branch `main`

## ⚠ CRITICAL: Always use `-p jojo-homelab` on every minikube command

There are two minikube profiles: `jojo-homelab` (running) and `minikube` (stopped default).
Any `minikube` command without `-p jojo-homelab` silently targets the stopped profile — the
image load appears to succeed but the image never reaches the cluster. This causes pods to
silently keep running the old code with no error.

## Steps (always in this order)

```bash
# 1. Build both images from project root
docker build -t gamilist-backend:latest ./backend
docker build -t gamilist-frontend:latest ./frontend

# 2. Load images into every cluster node — -p jojo-homelab IS REQUIRED
minikube image load gamilist-backend:latest -p jojo-homelab
minikube image load gamilist-frontend:latest -p jojo-homelab

# 3. Deploy via Helm
helm upgrade --install gamilist ./helm/gamilist \
  --kube-context jojo-homelab \
  --namespace gamilist \
  --create-namespace \
  --wait --timeout 3m

# 4. Force rollout restart (required — imagePullPolicy:Never + :latest tag means
#    Kubernetes won't restart pods automatically when a new image is loaded)
kubectl rollout restart deployment/frontend deployment/backend -n gamilist --context jojo-homelab
kubectl rollout status deployment/frontend deployment/backend -n gamilist --context jojo-homelab --timeout=90s

# 5. Verify the new bundle is actually live (frontend)
curl -s http://gamilist.local:8080/ | grep 'index-'
# The JS hash should be different from before — if it's the same, the old image is still running

# 6. Commit changed files (stage specific files, not -A)
git add <changed files>
git commit -m "..."
git push
```

## Common pitfalls

- **Wrong minikube profile:** Omitting `-p jojo-homelab` from `minikube image load` silently loads into the stopped default profile. Pods keep serving the old image with no error.
- **Stale Docker layer cache:** If the new bundle hash matches the old one after deploy, run `docker build --no-cache` to force a full rebuild.
- Do NOT use `minikube docker-env` — fails on multi-node clusters
- Always load images into minikube BEFORE running helm upgrade, otherwise pods get ImagePullBackOff
- `imagePullPolicy: Never` + `:latest` tag means Kubernetes never detects a new image — `helm upgrade` succeeds but pods keep running the old code. Always `kubectl rollout restart` after loading
- Helm chart lives at `./helm/gamilist` (not `helm/gamilist/gamilist`)

## If only backend changed

Skip the frontend build + load steps. Same applies in reverse.

## Verify deploy

```bash
# Pods should be Running with fresh AGE timestamps
kubectl get pods -n gamilist --context jojo-homelab

# Frontend: confirm new JS bundle hash is served
curl -s http://gamilist.local:8080/ | grep 'index-'

# Backend: confirm /api/list responds
curl -s http://gamilist.local:8080/api/list | head -5
```
