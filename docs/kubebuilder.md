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

1. re-run the controller `make run`

1. edit the `Foo` resource and change its `spec.foo` from `bar` to `baz` (just to "touch" it)

       k edit foo foo-sample

1. observe how "Reconciled" is logged again

## Add status

_TODO: Add additional fields.. to `api/v1/foo_types.go`` and [re-generate the CRD YAML with `make`](https://book.kubebuilder.io/cronjob-tutorial/gvks.html#but-why-create-apis-at-all)..._

1. run `k get foo foo-sample -o yaml` and notice the new `status`
