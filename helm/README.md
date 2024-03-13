# Installing the ARC helm chart

```
helm install arc \
    --namespace arc-systems \
    -f arc-controller-values.yaml \
    oci://ghcr.io/actions/actions-runner-controller-charts/gha-runner-scale-set-controller
```

### Only use if using Anthos/Istio
`kubectl label namespace arc-systems istio-injection=enabled`
`kubectl rollout restart deployment -n arc-systems`


## Upgrading the helm deployment
```
helm upgrade arc \
    --namespace arc-systems \
    -f arc-controller-values.yaml \
    oci://ghcr.io/actions/actions-runner-controller-charts/gha-runner-scale-set-controller
```

## Uninstalling the helm chart
`helm uninstall arc -n arc-systems`
---

# Installing the ARC runner set

```
helm install arc-runner-set \
    --namespace arc-runners \
    -f helm-base.yaml \
    oci://ghcr.io/actions/actions-runner-controller-charts/gha-runner-scale-set
```

### Only use if using Anthos/Istio
`kubectl label namespace arc-runners istio-injection=enabled`
`kubectl rollout restart deployment -n arc-runners`

## Upgrading the helm deployment
```
helm upgrade arc-runner-set \
    oci://ghcr.io/actions/actions-runner-controller-charts/gha-runner-scale-set \
    --namespace arc-runners \
    -f helm-base.yaml
```

## Uninstalling the helm chart
`helm uninstall arc-runner-set --namespace arc-runners`

## Annotate the kubernetes service account for ARC to the GCP service account to allow access to commands
```
kubectl annotate serviceaccount arc-runner-set-gha-rs-no-permission \
  -n arc-runners \
  iam.gke.io/gcp-service-account=github-runner-account@pearson-mojo-non-prod.iam.gserviceaccount.com
```