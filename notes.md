# Kubernetes
- Source: [Kubernetes Troubleshooting](https://twitter.com/danielbryantuk/status/1492893332850237444?s=28)
- If a container gets stuck in a crash-loop-backoff, use the `logs --previous` flag

$ kubectl logs my-pod -c my-container --previous
- `kubectl port-forwarding` can be useful, whether it's to check if an app is responding or to expose a remote dashboard locally (I frequently use port-forwards to look at the Argo CD dashboard!)

$ kubectl port-forward my-pod 8080:8080
- When I need more flexibility to poke around the cluster network, I use the @CloudNativeFdn Telepresence tool to "put my laptop in the cluster" 

$ telepresence connect 

$ curl my-service.my-namespace:port/path 

More info -> https://getambassador.io/docs/telepresence/latest/quick-start/
- If you want to spin up a service locally and run and debug it like it was in the cluster, Telepresence helps here too (and can route remote traffic, volumes, and envs locally)  

$ telepresence intercept my-service --port XX --mount=/tmp/
- If all else fails, and you're not using distroless containers then `kubectl exec` can be useful to poke around in the container in the cluster (but remember, this is like SSHing into prod!)

$ kubectl exec my-pod -c my-container -- /bin/sh
