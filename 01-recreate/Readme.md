#### Recreate Strategy nothing fancy
```bash
kubectl apply -f 01-deployment.yaml 
kubectl get pods -w
kubectl get pods -w
kubectl apply -f 02-deployment.yaml 
kubectl get pods -w
kubectl get pods -w
kubectl get pods -w
```

#### cleanup
```bash
kubectl delete -f 02-deployment.yaml
```
