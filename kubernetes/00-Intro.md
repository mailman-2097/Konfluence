# Introduction

This series will help you get started with Kubernetes aka K8s and provide a brief overview of the key concepts

# Overview of K8s Architecture

In brief the aspects of K8s are identified as follows:

1. The cluster will have a master node that hosts all the management components
1. Varius Worker Nodes can be spun up host the the pods
1. Pods will have the docker container applications
1. In order to achieve high availability and fault tolerance pods for the same deployment should run across multiple worker nodes

<IMG  src="https://miro.medium.com/max/875/1*h26nFoT4C8J_jt8ZyUReFA.png"/>

# Container Images and Registries

Container Images which are the application images once built need to be hosted to a image registry such that that can be applications can be deployed and managed through the software development lifecycle
<IMG  src="https://access.redhat.com/webassets/avalon/d/OpenShift_Container_Platform-4.3-Architecture-en-US/images/7cb0013c7080c715e106f482eab98065/create-push-app.png"  alt="Creating and pushing a containerized application"/>

# Talking to Kubernetes CLuster
You can interact with the cluster in the following ways:

1. Using the CLuster Dashboard or UI
1. Using the [Kubetctl](https://kubernetes.io/docs/tasks/tools/) Command line tool

## Note on Imperative vs Declarative
### Imperative Approach
Here the user uses kubectl command line tool to execute
```
kubectl run nginx --image=nginx --restart=Never
```
### Declarative Approach
Here the user uses kubectl command line tool to execute
```
cat > /home/$USER/pod.yaml << EOL
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec: 
  containers:
    - name: nginx-container
      image: nginx:latest
EOL

kubectl create -f /home/$USER/pod.yaml
```

# Kubernetes in Production
Inorder to run k8s in production one should utilise a managed services. Both Azure and AWS provides cloud native offerings.

Additionally, Openshift which is a commercial offering from Redhat can be leveraged for deployment of Kubernetes On premise Servers or VMware Hypervisor. Openshift is also available as PAAS offerings on Azure and AWS.

# Further Reading
You can review the following article that provides a more detailed overview of the various components within a k8s cluster environment
[A beginner friendly introduction to Kubernetes](https://towardsdatascience.com/a-beginner-friendly-introduction-to-kubernetes-540b5d63b3d7)

There are plenty of books, online video courses that you can leverage.

