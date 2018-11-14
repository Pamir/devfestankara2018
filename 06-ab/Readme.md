```bash
kubectl apply -f 01-deployment.yaml 
kubectl apply -f 02-deployment.yaml 
kubectl apply -f app-destination-rule.yaml 
kubectl apply -f app-virtual-service.yaml 
```

```bash
kubectl exec -it nettools  -n default -- /bin/sh
while true; do curl --connect-timeout 1 -m 1  -H "CLIENT_IP: 10.100.200.13" http://myapp.app; done
while true; do curl --connect-timeout 1 -m 1   http://myapp.app; done
```
