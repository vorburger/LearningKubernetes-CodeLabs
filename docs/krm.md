# Kubernetes Resource Model (KRM)

Kubernetes has a uniform Resource Model for all interactions you'll have with its API - the KRM. Let's explore it:

1. Get rid of the initial [hello, world](hello-world.md):

       k delete deployment echoserver

1. Glance at, and then _apply,_ the [echo.pod.yaml](files/echo.pod.yaml) _resource_ of `kind: Pod`:

       k apply -f https://raw.githubusercontent.com/vorburger/LearningKubernetes-CodeLabs/develop/docs/files/echo.pod.yaml

1. You now have a _`Pod`_ running. Let's list it, look at its log, and look at it's YAML:

       k get pods
       k logs echoserver
       k get pod echoserver -o yaml

   Note how the YAML shown is an extended version of the [echo.pod.yaml](files/echo.pod.yaml), which we _applied_ above, now with:

   * some new `metadata` (like a `creationTimestamp` or a `uid`)
   * additional `spec` (like system defaults; we could override those)
   * the `status`, which Kubernetes added when it _reconciled_ the _desired_ state (AKA _intent)_ expressed by the `spec` with the system's `observed` state

1. This _Pod_ is a (built-in) KRM API resource "kind" (type). We can see all of them like this:

       k api-resources
       k api-versions

1. We can learn more about each of them, as well as detailed documentation about the respective resource's fields:

       k explain pod
       k explain pod.spec.containers.image

1. Clean up:

       k delete pod echoserver
