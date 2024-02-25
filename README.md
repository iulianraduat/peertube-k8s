# peertube-k8s

PeerTube as k8s deployment

## Install

In the folder were you have all .yaml files run the following command:

```
kubectl apply -k .
```

If it does not work for minikube then try:

```
minikube kubectl apply -k .
```

If it does not work for microk8s then try:

```
microk8s kubectl apply -k .
```

You should see in the `default` namespace defined for kubernetes all the new objects.
The corresponding service is called `peertube`.

If you want to use it in a different namespace then just add "-n &lt;namespace&gt;" as argument to kubectl call.

You need to use a proxy in front of it (like nginx) to redirect to the exposed port on k8s node.
To find the mapped ports for port 9000 just check the "Internal Endpoints" of the service "peertube"
or run `kubectl get svc` from the shell of the server running the cluster.

Customize and copy the `config/production.yaml` file in the folder correspondig to the PVC `peertube-config`.
Without it, peertube cannot start.

Please configure your peertube to stream via http so you do not need to use one port per station.

## Notice

The .yaml files are generated from the docker-compose.yml of the specified release.

The pod for `peertube` runs four containers inside.

The `config/default.yaml` file is here only for reference.

The `postfix` part was not tested, so if there are errors please submit an PR for the fixes. Thanks.
