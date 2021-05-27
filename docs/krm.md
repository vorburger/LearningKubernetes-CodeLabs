# Kubernetes Resource Model (KRM)

Kubernetes has a uniform Resource Model for all interactions you'll have with its API - the KRM. Let's explore it:

1. Get rid of the initial [hello, world](hello-world.md):

       k delete deployment echoserver

1. Glance at, and then _apply,_ the [echo.pod.yaml](files/echo.pod.yaml):

       k apply -f https://raw.githubusercontent.com/vorburger/LearningKubernetes-CodeLabs/develop/docs/files/echo.pod.yaml

1. You now have a _`Pod`_ running. Let's list it, look at its log, and look at it's YAML:

       k get pods
       k logs echoserver
       k get pod echoserver -o yaml

   Note how the YAML file shown is an extended version of the [echo.pod.yaml](files/echo.pod.yaml) which we _applied_. The additional fields are what the Kubernetes added to it when it _reconciled_ the _intent_ expressed by our original YAML.

1. Clean up:

       k delete pod echoserver