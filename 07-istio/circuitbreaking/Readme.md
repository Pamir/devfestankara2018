#### Deploy Application
```bash
kubens app
kubectl apply -f 01-deployment.yaml
kubectl apply -f 02-deployment.yaml
kubectl apply -f app-destination-rule.yaml
kubectl apply -f app-virtual-service.yaml
```


```yaml
host: myapp
  trafficPolicy:
    connectionPool:
      tcp:
        maxConnections: 1
      http:
        http1MaxPendingRequests: 1
        maxRequestsPerConnection: 1
    outlierDetection:
      consecutiveErrors: 1
      interval: 1s
      baseEjectionTime: 3m
      maxEjectionPercent: 100
```

#### Run fortiO
```bash
kubectl apply  -f samples/httpbin/sample-client/fortio-deploy.yaml
kubectl exec -it $FORTIO_POD  -c fortio /usr/bin/fortio -- load -c 1 -qps 0 -n 20 -loglevel Warning http://myapp.app
kubectl exec -it $FORTIO_POD  -c fortio /usr/bin/fortio -- load -c 2 -qps 0 -n 20 -loglevel Warning http://myapp.app
kubectl exec -it $FORTIO_POD  -c fortio /usr/bin/fortio -- load -c 2 -qps 0 -n 20 -loglevel Warning http://myapp.app
```
