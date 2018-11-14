#### Rolling Update
```bash
kubectl run --restart=Never --image=raesene/alpine-nettools nettools
kubectl exec -it nettools -- /bin/sh
kubectl apply -f 01-deployment.yaml 
while true; do curl --connect-timeout 1 -m 1 http://my-app; done
kubectl apply -f 02-deployment.yaml 
```

#### cleanup
```bash
kubectl delete -f 02-deployment.yaml
```
