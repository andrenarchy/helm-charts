# helm-charts

Some Helm charts for Kubernetes that I use personally. Or at work. Or both.

## Setup

```
helm repo add andrenarchy https://andrenarchy.github.io/helm-charts/
```

## Notes
* Several Helm charts are forked from the deprecated [k8s-at-home](charts/vaultwarden/README.md) repository.
* The Helm charts are very lean by using the `common` [library-chart](https://github.com/k8s-at-home/library-charts).
* Uses [chart-releaser-action](https://github.com/helm/chart-releaser-action) to automatically release new charts from the `main` branch.

