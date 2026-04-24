# deploy skill

Deploys changes to the jojo-homelab Kubernetes cluster and pushes to GitHub. Encodes the full build → load → helm → git sequence so Claude doesn't re-discover it each session.

## Installation

```bash
cp deploy.md ~/.claude/skills/deploy.md
```

## Usage

```
/deploy
```

## What it does

1. Builds `gamilist-backend` and `gamilist-frontend` Docker images locally
2. Loads images into all nodes of the `jojo-homelab` minikube cluster via `minikube image load`
3. Runs `helm upgrade --install` with the `./helm/gamilist` chart
4. Commits changed files and pushes to `main`

## Why

The cluster uses a 3-node minikube setup with Docker driver and `imagePullPolicy: Never`. This combination means `minikube docker-env` doesn't work (multi-node limitation) and images must be explicitly loaded before deploying. Without this skill, Claude wastes turns figuring out why `docker-env` fails and how images get onto the nodes.
