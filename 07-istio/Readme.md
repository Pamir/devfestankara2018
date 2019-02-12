#### Istio installation
```bash
kubectl apply -f install/kubernetes/helm/istio/templates/crds.yaml
kubectl create clusterrolebinding cluster-admin-binding     --clusterrole=cluster-admin   \
    --user=$(gcloud config get-value core/account)
kubectl apply -f install/kubernetes/istio-demo.yaml
```

#### Apps installation
```bash
kubectl create ns app
kubectl label namespace app  istio-injection=enabled
kubectl apply -f 01-deployment.yaml -n app
kubectl apply -f 02-deployment.yaml -n app
kubectl exec -it nettools -- /bin/sh
while true; do curl --connect-timeout 1 -m 1 http://myapp.app; done
```

Istio integration

```bash

```
