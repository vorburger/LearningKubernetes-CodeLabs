# Fun & useful Kubernetes CLI enhancements

## kubecolor

Use https://github.com/dty1er/kubecolor to bring some color to your bland `kubectl` output:

    sudo apt install -y kubecolor

    alias k=kubecolor

    k get pods

## kubectx & kubens

Use https://github.com/ahmetb/kubectx (together with https://github.com/junegunn/fzf) to
easily switch between the different contexts and their default namespaces in your `~/kube/config`:

    sudo apt install -y fzf kubectx

    kubectx --help
    kubens --help

## TUIs

Following are some "[Midnight (Norton) Commander](https://en.wikipedia.org/wiki/Midnight_Commander)"-like
"[text-based user interfaces](https://en.wikipedia.org/wiki/Text-based_user_interface) (TUI).

### kubecom

Use https://github.com/AnatolyRugalev/kube-commander
with its [hotkeys based keyboard navigation](https://github.com/AnatolyRugalev/kube-commander#hotkeys)
like `D` for `kubectl describe` and `E` for `kubectl edit` or `L` for a Pod's logs, etc.

### kubebox

Use https://github.com/astefanutti/kubebox for a similar tool focused on Pods resource monitoring;
kubebox is particularly useful if your Kubernetes cluster has https://github.com/google/cadvisor.
