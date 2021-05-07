# Install Kubernetes

To follow the lessons in this tutorial, you need to have the following prerequisites:

1. a Kubernetes cluster
1. configuration to access it (in a `~/.kube/config` file)
1. the `kubectl` CLI binary, aliased to `k`

There are many ways to set this up. One of easiest ways to get started is to use https://minikube.sigs.k8s.io/docs/start, and:

    minikube start
    alias k="minikube kubectl -- "

Alternatives include e.g. `kind`, `kubeadm`; or cloud hosted managed Kubernetes offerings like Google's GKE; or local distributions like k3s.io, k3s.io, OpenShift, et al. We may add documentation about such other approaches later.
