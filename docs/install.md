# Install Kubernetes

To follow the lessons in this tutorial, you need to have the following prerequisites:

1. a Kubernetes cluster
1. configuration to access it (in a `~/.kube/config` file)
1. the `kubectl` CLI binary, aliased to `k`

There are several ways to set this up, see the options below. Alternatives include e.g. `kind`, `kubeadm`; or cloud hosted managed Kubernetes offerings like Google's GKE; or local distributions like k3s.io, k3s.io, OpenShift, et al. (We may add documentation about such other approaches later.)


## minikube Docker driver

One of easiest ways to get started on a developer workstation is to use https://minikube.sigs.k8s.io/docs/start, and:

    minikube start
    alias k="minikube kubectl -- "

This creates a VM, and works equally well on Windows, Mac and Linux.


## minikube None driver

To avoid creating a VM and run the Kubernetes control panel containers straight on the host,
which is suitable e.g. inside a new Linux VM which isn't used for anything else, use the 
_[Linux "none" (= bare-metal) driver](https://minikube.sigs.k8s.io/docs/drivers/none/)_,
e.g. with Debian 10 simply:

    sudo apt-get install conntrack
    sudo sysctl fs.protected_regular=0

    curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
    sudo install minikube-linux-amd64 /usr/local/bin/minikube
    sudo -E minikube start --driver=none

    sudo chown -R $(id -un):$(id -gn $(id -un)) /home/vorburger_google_com/.minikube/
    alias k="minikube kubectl -- "


## Test Installation

The goal of each of the set-up options above, if successful, is that you should be able to run:

    k get pods -A
    
and see:

    NAMESPACE     NAME                               READY   STATUS    RESTARTS   AGE
    kube-system   coredns-74ff55c5b-mdlfl            1/1     Running   0          1d
    kube-system   etcd-vm-test2                      1/1     Running   0          1d
    kube-system   kube-apiserver-vm-test2            1/1     Running   0          1d
    kube-system   kube-controller-manager-vm-test2   1/1     Running   0          1d
    kube-system   kube-proxy-9m598                   1/1     Running   0          1d
    kube-system   kube-scheduler-vm-test2            1/1     Running   0          1d
    kube-system   storage-provisioner                1/1     Running   0          1d
