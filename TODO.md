# ToDo

- [ ] [`kind`](https://kind.sigs.k8s.io/docs/user/quick-start/) (and [here](https://book.kubebuilder.io/reference/kind.html)) as another Kubernetes "distributions" than `minikube` in [docs/install.md](docs/install.md)

- [ ] contribute https://github.com/vorburger/LearningKubernetes-CodeLabs/blob/develop/docs/kubebuilder.md to https://book.kubebuilder.io as simpler first lesson before the full-blown cronjob example.

- [ ] Additional New Lessons

  - [ ] API: Run Foo Controller against https://github.com/kcp-dev/kcp instead of "real" (mini)kube
  - [ ] https://sdk.operatorframework.io (https://github.com/operator-framework/operator-sdk)
  - [ ] Testing controllers? https://book.kubebuilder.io/cronjob-tutorial/writing-tests.html

  - [ ] API: OpenAPI schema in separate file outside of CRD YAML, so that it's validated by super-linter's `VALIDATE_OPENAPI`
  - [ ] API: Generate OpenAPI schema from ProtoBuf PB? See https://cuelang.org/docs/integrations/protobuf/ and https://cuelang.org/docs/integrations/openapi/

  - [ ] https://googlecontainertools.github.io/kpt/
  - [ ] https://fluxcd.io
  - [ ] https://shipwright.io

  - [ ] https://github.com/prometheus-operator/kube-prometheus#installing
  - [ ] https://github.com/prometheus-operator/prometheus-operator

  - [ ] Users Management via CRD
  - [ ] https://cert-manager.io

  - [ ] https://github.com/kvaps/kubectl-build (or https://github.com/vmware-tanzu/buildkit-cli-for-kubectl)
  - [ ] https://BuildPacks.io, see [KubeCon Prez](https://static.sched.com/hosted_files/kccnceu2021/f3/IntroductionToCloudNativeBuildpacks_StephenLevineJesseBrown_v1.pdf)
  - [ ] https://github.com/kvaps/kubectl-node-shell (+ https://github.com/containers/toolbox ?)
  - [ ] https://knative.dev
  - [ ] https://www.openfaas.com
  - [ ] https://k8slens.dev

- [ ] Listen in to [Kubebuilder, Controller Runtime, and Controller Tools Meeting](https://docs.google.com/document/d/1Ih-2cgg1bUrLwLVTB9tADlPcVdgnuMNBGbUl4D-0TIk/)
 
- [ ] Use https://github.com/monopole/mdrip to validate the lessons! (And add a "used by" section to its README.)
  Contribute the same to kubebuilder, see https://github.com/kubernetes-sigs/kubebuilder/issues/711

- [ ] Other Kubernetes distributions than `minikube`:

  - [ ] kubeadm.. on CoreOS?
  - [ ] https://k3s.io (https://k3d.io)
  - [ ] https://github.com/rootless-containers/usernetes
  - [ ] https://microk8s.io
  - [ ] https://k0sproject.io

- [ ] CoreOS instead of Debian on GCP: Debian works, but CoreOS SSH keys are somehow missing:
  (update https://docs.fedoraproject.org/en-US/fedora-coreos/provisioning-gcp/)

      gcloud compute instances create kubernetes-codelab --zone europe-west4-c --min-cpu-platform "Intel Haswell" --image-project debian-cloud --image-family debian-10
      gcloud compute ssh kubernetes-codelab

      gcloud compute instances create coreos2 --zone europe-west4-c  --min-cpu-platform "Intel Haswell" --image-project fedora-coreos-cloud --image-family fedora-coreos-next
      gcloud compute ssh core@coreos2
      Using OS Login user [$USER] instead of requested user [core]
      $USER@$IP: Permission denied (publickey,gssapi-keyex,gssapi-with-mic).

      gcloud compute instances create coreos1 --zone europe-west4-c --min-cpu-platform "Intel Haswell" --image-project fedora-coreos-cloud --image-family fedora-coreos-stable
      gcloud compute ssh coreos1
      $YOU@$IP: Permission denied (publickey,gssapi-keyex,gssapi-with-mic).

      gcloud compute ssh core@coreos1
      Using OS Login user [$YOU] instead of requested user [core]

      ssh: connect to host $IP port 22: Connection timed out
      ERROR: (gcloud.compute.ssh) [/usr/bin/ssh] exited with return code [255].

- [ ] https://github.com/googlecodelabs/tools ?

- [ ] https://codelabs.developers.google.com ?
