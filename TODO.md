- [ ] Lessons:

  - [ ] API: Build a Controller (Operator?)
  - [ ] API: OpenAPI schema in separate file outside of CRD YAML, so that it's validated by super-linter's `VALIDATE_OPENAPI`
  - [ ] API: Generate OpenAPI schema from ProtoBuf PB? See https://cuelang.org/docs/integrations/protobuf/ and https://cuelang.org/docs/integrations/openapi/

  - [ ] https://googlecontainertools.github.io/kpt/

  - [ ] https://github.com/kvaps/kubectl-build (or https://github.com/vmware-tanzu/buildkit-cli-for-kubectl)
  - [ ] https://BuildPacks.io, see [KubeCon Prez](https://static.sched.com/hosted_files/kccnceu2021/f3/IntroductionToCloudNativeBuildpacks_StephenLevineJesseBrown_v1.pdf)
  - [ ] https://github.com/kvaps/kubectl-node-shell (+ https://github.com/containers/toolbox ?)
  - [ ] https://knative.dev
  - [ ] https://www.openfaas.com

- [ ] Other Kubernetes distributions than `minikube`:

  - [ ] kubeadm
  - [ ] kind
  - [ ] https://github.com/rootless-containers/usernetes
  - [ ] https://microk8s.io
  - [ ] https://k3s.io (https://k3d.io)
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

- [ ] GitHub Action (pre-commit hook) to lint all markdown, check links, etc.

- [ ] https://github.com/googlecodelabs/tools ? 

- [ ] https://codelabs.developers.google.com ?
