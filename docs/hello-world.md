# hello, world

Whatever [Kubernetes Installation](install.md) you use, here is a first example how to use it,
inspired by [Kubernetes' tutorial](https://kubernetes.io/docs/tutorials/stateless-application/expose-external-ip-address/)
or [GKE's Quickstart](https://cloud.google.com/kubernetes-engine/docs/quickstart).

## [echoserver](https://github.com/kubernetes/kubernetes/tree/master/test/images/echoserver)

    $ k create deployment echoserver --image=k8s.gcr.io/echoserver:1.10
    $ k expose deployment echoserver --type=LoadBalancer --port=8080
    $ k get service echoserver
    NAME         TYPE           CLUSTER-IP   EXTERNAL-IP     PORT(S)          AGE
    echoserver   LoadBalancer   10.x.y.z     a.b.c.d         8080:32151/TCP   1m

The `echoserver` web page is now available at http://a.b.c.d:8080.
If the external IP address is still shown as _"pending",_ then wait for a minute and retry.
BTW when using [`minikube`](install.md#minikube) there may not be an `EXTERNAL-IP`, then you have to use `minikube service` instead:

    $ minikube service --url=true echoserver

Execute the following commands to have a look at what Kubernetes created based on the commands above:

    $ k describe service echoserver
    $ k get -o yaml service echoserver
    $ k describe deployment echoserver
    $ k get -o yaml deployment echoserver
    $ k describe replicaset echoserver
    $ k get -o yaml replicaset
    $ k get -o yaml pod
    $ k describe pod echoserver
    (...)
    Limits:
      cpu:                500m
      ephemeral-storage:  1Gi
      memory:             2Gi

Note how the CPU, Memory and Storage Limits were automatically chosen. In a next step, you'll want to set more appropriate limits yourself.
To remove this first example from your cluster, clean up both the service and deployment, which will also remove its replicaset and pod:
    
    $ k delete service echoserver
    $ k delete deployment echoserver

## Dashboard for Minikube

    minikube dashboard

If you run `minikube` inside a Virtual Machine (VM) instead of on your Laptop/Desktop workstation,
then you'll need to set up some port forwarding to be able to access services in your local web browser.
