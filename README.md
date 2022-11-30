# HiveCloud microcloud

As a (fake) cloud company we provide some services services proposed by the [CNCF](https://landscape.cncf.io/) like OpenFaaS, Kubernetes, LXC containers, and more.

Here is the documentation of what we deployed.

# Kubernetes

Because we work on single node we chose to use `microk8s` as our kubernetes distribution thanks to it simplicity and scalability.

## Deploy microk8s

Install the package:

`sudo snap install microk8s --classic`

Enable the required services:

`microk8s enable dashboard dns registry istio`

And verify the availability

`microk8s status`

## Accessing the dashboard

As enabled previously we can now access the kubernetes dashboard:

`microk8s dashboard-proxy`

![Dashboard](./images/kube-dashboard.png)

## Deploy weave scope

To have a better view of our kubernetes cluster we use `weave scope` to monitor our services and pods.

Deploy weave scope:

`kubectl apply -f https://github.com/weaveworks/scope/releases/download/v1.13.2/k8s-scope.yaml`

Acces the dashboard:

`kubectl port-forward -n weave "$(kubectl get -n weave pod --selector=weave-scope-component=app -o jsonpath='{.items..metadata.name}')" 4040`

![Dashboard](./images/weave-dashboard.png)