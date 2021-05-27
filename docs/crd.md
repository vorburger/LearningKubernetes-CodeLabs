# Kubernetes Custom Resource Definition (CRD)

One of [the ways to extend Kubernetes](https://kubernetes.io/docs/tasks/extend-kubernetes/)
is to write [your own Custom Resource Definition](https://kubernetes.io/docs/tasks/extend-kubernetes/custom-resources/custom-resource-definitions/) (CRD). This allows you to extend [the KRM](krm.md) with your own "types", like this:

1. Let's first look at the _built-in_ KRM API resource "types", and note e.g. the _Pod_ we used in [the previous lesson](krm.md):

        k api-resources

1. Glance at, and then _apply,_ the [foo.crd.yaml](files/foo.crd.yaml):

       k apply -f https://raw.githubusercontent.com/vorburger/LearningKubernetes-CodeLabs/develop/docs/files/foo.crd.yaml

1. This has created a new (custom) KRM API resource kind, named _foo_. It now appears on the API:

       k api-resources | grep foo

       k explain foo
       k explain foo.spec

1. We can now create a new resource of this kind, e.g. by applying the [hello.foo.yaml](files/hello.foo.yaml):

       k apply -f https://raw.githubusercontent.com/vorburger/LearningKubernetes-CodeLabs/develop/docs/files/hello.foo.yaml

1. You now have a _`Foo`_. Let's list it, look at it's YAML:

       k get foos
       k get foo hello -o yaml

1. Try to edit it, and change "xyz" from "7" to "13", and not the validation error you'll get, xyz =< 10:

       k edit foo hello

1. Clean up:

       k delete foo hello
