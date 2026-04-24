# Deploy Skill

Deploy changes to the jojo-homelab Kubernetes cluster and push to GitHub.

## Cluster facts

- **Minikube profile:** `jojo-homelab` (3-node cluster)
- **Driver:** Docker — multi-node, so `minikube docker-env` does NOT work
- **Image loading:** Build locally with `docker build`, then load with `minikube image load`
- **Image pull policy:** `Never` — images must be present on nodes before helm upgrade
- **Helm chart:** `./helm/gamilist`, namespace `gamilist`
- **Images:** `gamilist-backend:latest`, `gamilist-frontend:latest`
- **Git remote:** `github.com:jojo-homelab/gamilist.git`, branch `main`

## Steps

Run in order from the project root:

### 1. Build images

```bash
docker build -t gamilist-backend:latest ./backend
docker build -t gamilist-frontend:latest ./frontend
```

If only one service changed, skip the build for the other.

### 2. Load images into the cluster

```bash
minikube image load gamilist-backend:latest -p jojo-homelab
minikube image load gamilist-frontend:latest -p jojo-homelab
```

### 3. Deploy via Helm

```bash
helm upgrade --install gamilist ./helm/gamilist \
  --kube-context jojo-homelab \
  --namespace gamilist \
  --create-namespace \
  --wait --timeout 3m
```

### 4. Commit and push

```bash
git add <changed files>
git commit -m "..."
git push
```

## Verify

```bash
kubectl get pods -n gamilist --context jojo-homelab
```

All pods should be `Running` with fresh `AGE` timestamps.

## Common pitfalls

- Never use `minikube docker-env` — it fails on multi-node clusters
- Always load images before `helm upgrade` — stale or missing images cause `ImagePullBackOff`
- Stage specific files with `git add`, not `-A`, to avoid accidentally committing secrets or large binaries
