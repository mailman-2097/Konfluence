[[_TOC_]]

# Introduction
This tutorial provides a quick introduction into Kubernetes aka K8s and how to setup a local development environment to experiment.

# Local Development Environment Setup

## Installing a local VM (Recommended)
It is recommended to install cluster and cluster management tools on a local virtual machine, but this is optional.
> You can refer to the following repo to get a working vagrant vm setup
https://git.health.nsw.gov.au/60278807/vagrant-ubuntu22

## Installing Docker
Installing Docker will be a pre-requisite such that you can build and manage container images as follows:
1. Docker images can be built from the command line
1. Local Docker images once built can be pushed to [docker hub](https://hub.docker.com/) which is a public image registry
1. Alternatively, public docker images can be pulled and deployed

[Getting Started with Docker](https://www.docker.com/get-started/)

Installing docker can be done in two ways:

1. Installing the docker engine in your VM or 
1. Utilise the newer Docker Desktop client.

[Installation instructions for Docker Engine and desktop are available here](https://docs.docker.com/engine/install/)

## Installing Minikube
Minikube is a lightweight cluster environment where you can try out most of the features of K8s. It is quite easy to setup. Installing a full blown k8s setup is not required.

Minikube can be installed locally in the following ways:
1. On your local Linux VM running on Virtual box

``` 
# Ubuntu VM Install
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
minikube start
```

2. for Linux or Windows installation instractions please refer to vendor documentation
[Installation instructions for Minikube on all available OS types](https://minikube.sigs.k8s.io/docs/start/)

## Installing Kubectl

Kubectl is a commandline line utility that you can use to manage your kubernetes cluster

Its available inbuilt within minikube 

[Kubectl with Minikube](https://minikube.sigs.k8s.io/docs/handbook/kubectl/)

or can be installed seperately

[Kubectl Standalone](https://kubernetes.io/docs/tasks/tools/)

``` 
# Ubuntu VM Install
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
curl -LO "https://dl.k8s.io/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
kubectl version --client --output=yaml
```

## Kind as an alternative to Minikube

Unlike Minikube which is a monolithic installation i.e. all the k8s components are combined into one Master cum Worker Node. Kind allows you to setup a more traditional multinode cluster locally i.e. master and multiple worker nodes for trying out some scenarios that cannot be done on minikube.

[Getting Started with Kind](https://kind.sigs.k8s.io/docs/user/quick-start/)

``` 
# Ubuntu VM Install
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.14.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind

cat > ~/.kube/kind_cluster << EOL
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
- role: worker
- role: worker
EOL

kind create cluster --config ~/.kube/kind_cluster
```