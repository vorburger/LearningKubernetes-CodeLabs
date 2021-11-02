# Install Kubernetes

To follow the lessons in this tutorial, you need to have the following prerequisites:

1. a Kubernetes cluster
1. configuration to access it (in a `~/.kube/config` file)
1. the `kubectl` CLI binary, aliased to `k`

There are different ways to set this up - pick one of the options below! (Alternatives include e.g. `kind`, `kubeadm`, k3s.io, microk8s.io, OpenShift, and others; we may add documentation about them later.) If you play with several of these, then [kubectx](fun/kubectx-kubens.md) is handy.

## Local (or VM) Installations

### minikube

One of easiest ways to get started on a developer workstation is to use https://minikube.sigs.k8s.io/docs/start, and:

    minikube start
    alias k="minikube kubectl -- "

This typically creates a VM, and works equally well on Windows, Mac and Linux.

### minikube None driver

To avoid creating a VM and run the Kubernetes control panel containers straight on the host,
which is suitable e.g. inside a new Linux VM which isn't used for anything else, use the
_[Linux "none" (= bare-metal) driver](https://minikube.sigs.k8s.io/docs/drivers/none/)_,
e.g. with Debian 10 simply:

    sudo apt-get install conntrack
    sudo sysctl fs.protected_regular=0

    curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
    sudo install minikube-linux-amd64 /usr/local/bin/minikube
    sudo -E minikube start --driver=none

    sudo chown -R $(id -un):$(id -gn $(id -un)) ~/.kube/
    sudo chown -R $(id -un):$(id -gn $(id -un)) ~/.minikube/
    alias k="minikube kubectl -- "

## Cloud Installations

### Google Cloud Shell minikube

https://cloud.google.com/shell is an easy to use and ready-made VM which already includes Docker and Minikube, so you can simply:

1. open https://shell.cloud.google.com (or `gcloud cloud-shell ssh [--ssh-flag="-A"]`)
2. `minikube start`
3. `alias k="minikube kubectl -- "`

To be able to use e.g. GitHub by `ssh` from this shell, do:

     ln -s ~/.ssh/google_compute_engine ~/.ssh/id_rsa
     ln -s ~/.ssh/google_compute_engine.pub ~/.ssh/id_rsa.pub

### Google Kubernetes Engine (GKE)

See https://cloud.google.com/kubernetes-engine/docs/quickstart, after [having enabled billing](https://cloud.google.com/billing/docs/how-to/modify-project#confirm_billing_is_enabled_on_a_project):

    gcloud services enable container.googleapis.com
    gcloud --project=XXX container clusters create-auto cluster1 --zone=europe-west4
    gcloud container clusters get-credentials cluster1 --project=XXX --region=europe-west4

[Autopilot clusters accrue a flat fee of $0.10/h](https://cloud.google.com/kubernetes-engine/pricing) (=$75/month, $890/year), so  when you're done learning, don't forget to:

    gcloud container clusters delete cluster1

## Test the Installation

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
