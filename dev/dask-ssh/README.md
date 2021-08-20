# daskssh HELM CHART

## Quick start

### Requirements

- Kubernetes cluster
- Cert-Manager

### Minimal set of values

```yaml
```

### Deploy DODAS JupyterHUB

```bash
git clone
cd ./dev/dask-ssh

kubectl create namespace dask

helm upgrade --install --wait --cleanup-on-fail --namespace dask \
                    daskssh \
                    ./ \
                    --values /tmp/external_values.yaml
```

## Values

Below you will find the most common default settings. Please find the complete list [here]()

```yaml
```
