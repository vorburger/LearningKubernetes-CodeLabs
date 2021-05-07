# hello, world

## echoserver

    k create deployment echoserver --image=k8s.gcr.io/echoserver:1.10
    k expose deployment echoserver --type=LoadBalancer --port=8080
    curl $(minikube service --url=true echoserver)

<!-- TODO where is the source code of this echoserver? -->

## Dashboard

    minikube dashboard

If you run `minikube` inside a Virtual Machine (VM) instead of on your Laptop/Desktop workstation, then you'll need to set up some port forwarding to be able to access services in your local web browser.