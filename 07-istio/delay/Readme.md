#### Deploy Application
```bash
kubens app
kubectl apply -f 01-deployment.yaml
kubectl apply -f 02-deployment.yaml
kubectl apply -f app-destination-rule.yaml
kubectl apply -f app-virtual-service.yaml
```


```yaml
  http:
  - fault:
      delay:
        fixedDelay: 7s
        percent: 100
```

#### Run fortio
```bash
kubectl apply  -f samples/httpbin/sample-client/fortio-deploy.yaml
kubectl exec -it $FORTIO_POD  -c fortio /usr/bin/fortio -- load -c 1 -qps 0 -n 20 -loglevel Warning http://myapp.app
kubectl exec -it $FORTIO_POD  -c fortio /usr/bin/fortio -- load -c 2 -qps 0 -n 20 -loglevel Warning http://myapp.app
kubectl exec -it $FORTIO_POD  -c fortio /usr/bin/fortio -- load -c 2 -qps 0 -n 20 -loglevel Warning http://myapp.app
```
