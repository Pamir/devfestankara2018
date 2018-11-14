#### Metacontroller

[Metacontroller Documentation](https://metacontroller.app/) </br>
[Metacontroller Github](https://github.com/GoogleCloudPlatform/metacontroller)

##### Install Metacontroller
```bash
kubectl create clusterrolebinding pamir-cluster-admin-binding --clusterrole=cluster-admin --user=<user>@<domain>
kubectl apply -f https://raw.githubusercontent.com/GoogleCloudPlatform/metacontroller/master/manifests/metacontroller-rbac.yaml
kubectl apply -f https://raw.githubusercontent.com/GoogleCloudPlatform/metacontroller/master/manifests/metacontroller.yaml
```

#### Install BlueGreen Deployment Controller
```bash
kubectl create configmap bluegreen-controller -n metacontroller --from-file=sync.js
kubectl apply -f bluegreen-controller.yaml
```
#### Deployment
```bash
kubectl apply -f app-v1.yaml
kubectl exec -it nettools -- /bin/sh
while true; do curl --connect-timeout 1 -m 1 http://my-app; done
kubectl apply -f app-v2.yaml
```
#### cleanup
```bash
kubectl delete -f app-v2.yaml
```
