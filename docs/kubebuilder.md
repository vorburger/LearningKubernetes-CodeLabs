# Kubebuilder

https://kubebuilder.io, notably https://kubebuilder.io/quick-start.html,
and https://github.com/kubernetes-sigs/kubebuilder.

## Install kubebuilder

    curl -L -o kubebuilder https://go.kubebuilder.io/dl/latest/$(go env GOOS)/$(go env GOARCH)
    chmod +x kubebuilder && sudo mv kubebuilder /usr/local/bin/

    kubebuilder
    kubebuilder init --help

## Quick Start

    mkdir learning-kubebuilder && cd learning-kubebuilder
    kubebuilder init --domain vorburger.ch --repo github.com/vorburger/learning-kubebuilder --project-name learning-kubebuilder --owner "Michael Vorburger" --component-config true
    kubebuilder create api --group learning --kind Foo --version v1

    make install
    k api-resources | grep foo
    make run

    cat config/samples/*
    k apply -f config/samples/
    k get foo foo-sample -o yaml

Stop (Ctrl-C) the `make run` to clean-up.

## Modify Controller

_You may want to use your favourite Go IDE of choice instead of a text editor for the following code changes.
The web-based [Google Cloud Code](https://cloud.google.com/code), or [Gitpod](https://www.gitpod.io), both
based on [Eclipse Theia](https://theia-ide.org), are a great choice. Alternatives include e.g.
[VS Code](https://code.visualstudio.com), or your favourite TUI editor with LSP support._

1. edit the `controllers/foo_controller.go` and change the `Reconcile` function to look like this:

   ```go
   log := log.FromContext(ctx)

   var foo model.Foo
   if err := r.Get(ctx, req.NamespacedName, &foo); err != nil {
       log.Error(err, "Get failed")
       return ctrl.Result{}, client.IgnoreNotFound(err)
   }

   log.Info("Reconciled")
   return ctrl.Result{}, nil
   ```

1. re-run the controller with `make run`

1. edit the `Foo` resource and change its `spec.foo` from `bar` to `baz` (just to "touch" it)

       k edit foo foo-sample

1. observe how "Reconciled" is logged again

## Add status

1. make a backup of the initial CRD YAML (or use git diff in the step after the next):

       cp config/crd/bases/learning.vorburger.ch_foos.yaml config/crd/bases/learning.vorburger.ch_foos.original.yaml

1. edit the `api/v1/foo_types.go` and change the `type FooStatus struct` to look like this:

       type FooStatus struct {
           Bar string `json:"bar,omitempty"`
       }

1. re-generate the generated CRD YAML, and note how `bar` got added to `status`:

       make install
       diff config/crd/bases/learning.vorburger.ch_foos.yaml config/crd/bases/learning.vorburger.ch_foos.original.yaml

1. edit the `controllers/foo_controller.go` and change the `Reconcile` function to look like this:

   ```go
   log := log.FromContext(ctx)

   var foo model.Foo
   if err := r.Get(ctx, req.NamespacedName, &foo); err != nil {
       log.Error(err, "Get failed")
       return ctrl.Result{}, client.IgnoreNotFound(err)
   }

   foo.Status.Bar = "hello, " + foo.GetName() + " with spec " + foo.Spec.Foo
   if err := r.Status().Update(ctx, &foo); err != nil {
       log.Error(err, "Update failed")
       return ctrl.Result{}, err
   }

   log.Info("Reconciled")
   return ctrl.Result{}, nil
   ```

1. re-run the controller with `make run`

1. run `k get foo foo-sample -o yaml` and notice the new `status`

1. edit the `Foo` resource and change its `spec.foo` back from `baz` to `bar` (just to "touch" it)

       k edit foo foo-sample

1. re-run `k get foo foo-sample -o yaml` and notice the updated `status`
