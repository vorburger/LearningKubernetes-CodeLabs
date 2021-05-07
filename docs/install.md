# Install Kubernetes

To follow the lessons in this tutorial, you need to have the following prerequisites:

1. a Kubernetes cluster
1. configuration to access it (in a `~/.kube/config` file)
1. the `kubectl` CLI binary, aliased to `k`

There are several ways to set this up, see the options below. Alternatives include e.g. `kind`, `kubeadm`; or cloud hosted managed Kubernetes offerings like Google's GKE; or local distributions like k3s.io, k3s.io, OpenShift, et al. We may add documentation about such other approaches later.


## minikube Docker driver

One of easiest ways to get started on a developer workstation is to use https://minikube.sigs.k8s.io/docs/start, and:

    minikube start
    alias k="minikube kubectl -- "


## minikube None driver

Suitable e.g. for a new VM which isn't used for anything else, with Debian 10:

    sudo apt-get install conntrack
    sudo sysctl fs.protected_regular=0
    sudo -E minikube start --driver=none

    sudo chown $(id -un):$(id -gn $(id -un)) /home/vorburger_google_com/.minikube/profiles/minikube/*
    alias k="minikube kubectl -- "
