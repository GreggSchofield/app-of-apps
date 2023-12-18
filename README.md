# app-of-apps
Sandbox for bootstrapping a Kubernetes cluster using the ArgoCD app-of-apps pattern and GitOps

Create and sync the parent app (app of apps) via the `argocd` cli:

```shell
argocd app create app-of-apps \
    --dest-namespace argocd \
    --dest-server https://kubernetes.default.svc \
    --repo https://github.com/GreggSchofield/app-of-apps.git \
    --path apps
```

Sync the patent app to its target state via a label selector:

```shell
argocd app sync -l app.kubernetes.io/instance=app-of-apps
```