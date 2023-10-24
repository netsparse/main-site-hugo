---
layout: post
author: Angel
date: 2023-06-15T17:35:43-05:00
title: "Quick Kubernetes Hands-on Guide"
tags: ["kubernetes", "devops", "docker", "networking", "sysadmin"]
description:
showToc: true
TocOpen: false
hidemeta: false
comments: true
disableHLJS: false # to disable highlightjs
disableShare: true
hideSummary: false
searchHidden: false
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: false
draft: false
---

[Kubernetes](https://kubernetes.io/) is an open-source platform that is used for deploying, scaling, and managing containerized applications. It is a powerful tool that enables developers to create and manage complex distributed systems with ease.

Here's a quick overview from [Fireship.io](https://fireship.io/).

{{< ytlazy PziYflu8cB8 >}}

## Concepts

### Cluster

A Kubernetes cluster consists of a set of worker machines, called nodes, that run containerized applications. Every cluster has at least one worker node.

The worker node(s) host the Pods that are the components of the application workload. The control plane manages the worker nodes and the Pods in the cluster. In production environments, the control plane usually runs across multiple computers and a cluster usually runs multiple nodes, providing fault-tolerance and high availability.

This document outlines the various components you need to have for a complete and working Kubernetes cluster.

![img](https://d33wubrfki0l68.cloudfront.net/2475489eaf20163ec0f54ddc1d92aa8d4c87c96b/e7c81/images/docs/components-of-kubernetes.svg)

## Control Plane Components

The control plane's components make global decisions about the cluster, such as scheduling, detecting, and responding to cluster events (for example, starting up a new pod when a deployment's replicas field is unsatisfied).

### [kube-apiserver](https://kubernetes.io/docs/reference/command-line-tools-reference/kube-apiserver/)

The API server is a component of the Kubernetes control plane that exposes the Kubernetes API. The API server is the front end for the Kubernetes control plane.

### [etcd](https://kubernetes.io/docs/concepts/overview/components/#etcd)

Consistent and highly-available key value store used as Kubernetes' backing store for all cluster data.

### [kube-scheduler](https://kubernetes.io/docs/reference/command-line-tools-reference/kube-scheduler/)

Control plane component that watches for newly created Pods with no assigned node, and selects a node for them to run on.

### [cloud-controller-manager](https://kubernetes.io/docs/concepts/architecture/cloud-controller/)

A Kubernetes control plane component that embeds cloud-specific control logic. The cloud controller manager lets you link your cluster into your cloud provider's API, and separates out the components that interact with that cloud platform from components that only interact with your cluster.

## Node Components

Node components run on every node, maintaining running pods and providing the Kubernetes runtime environment.

### [kubelet](https://kubernetes.io/docs/reference/command-line-tools-reference/kubelet/) 

An agent that runs on each node in the cluster. It makes sure that containers are running in a Pod. 

### [kube-proxy](https://kubernetes.io/docs/reference/command-line-tools-reference/kube-proxy/)

A network proxy that runs on each node in your cluster, implementing part of the Kubernetes Service concept.

### [Container runtime](https://kubernetes.io/docs/setup/production-environment/container-runtimes/)

The container runtime is the software that is responsible for running containers.

Kubernetes supports container runtimes such as `containerd`, `CRI-O`, `rkt`, `frakti` and any other implementation of the [Kubernetes CRI (Container Runtime Interface)](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-node/container-runtime-interface.md).

However, most Kubernetes users deploy their applications using Docker.

## Getting Started

You can set up a cluster on your own hardware, or you can use a cloud-based service like [Google Kubernetes Engine (GKE)](https://cloud.google.com/kubernetes-engine/), [Amazon Elastic Kubernetes Service (EKS)](https://aws.amazon.com/eks/), or [Microsoft Azure Kubernetes Service (AKS)](https://azure.microsoft.com/en-us/products/kubernetes-service/).

We'll go ahead and utilize [minikube](https://minikube.sigs.k8s.io/docs/), which should provide us with a local Kubernetes cluster we can start with.

Make sure to check out the [Kubernetes guide](https://kubernetes.io/docs/tutorials/kubernetes-basics/create-cluster/cluster-intro/) or [minikube documentation](https://minikube.sigs.k8s.io/docs/start/) if you need more details.

### Requirements

- 2 CPUs or more
- 2GB of free memory
- 20GB of free disk space
- Internet connection
- Container or virtual machine manager, such as: Docker, QEMU, Hyperkit, Hyper-V, KVM, Parallels, Podman, VirtualBox, or VMware Fusion/Workstation


### Installation

We'll utilize the latest minikube **stable** release for Debian in this example.

```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube_latest_amd64.deb
sudo dpkg -i minikube_latest_amd64.deb
```

Once you have installed `minikube`, start your cluster:

```bash
minikube start
```

If you already have `kubectl` installed, you can now use it to access your shiny new cluster:

```bash
kubectl get po -A
```

Alternatively, minikube can download the appropriate version of kubectl and you should be able to use it like this:

```bash
minikube kubectl -- get po -A
```

You can also make your life easier by adding the following to your shell config:

```bash
alias kubectl="minikube kubectl --"
```

To set up `kubectl` to communicate with your Kubernetes cluster, you need to provide the cluster credentials in a configuration file. 

This file can be generated using the cloud provider's console or CLI tools.

```bash
kubectl config set-cluster my-cluster --server=https://my-cluster-url.com
kubectl config set-credentials my-cluster-user --username=my-username --password=my-password
kubectl config set-context my-cluster-context --cluster=my-cluster --user=my-cluster-user
kubectl config use-context my-cluster-context
```

The above commands set up a new cluster named `my-cluster`, add user credentials, create a new context, and switch to using the new context.

### Create a Deployment

```bash
kubectl create deployment hello-node --image=registry.k8s.io/e2e-test-images/agnhost:2.39 -- /agnhost netexec --http-port=8080
```

### Deploying a Single Container with a Manifest

To create a deployment using a `manifest file`, you will need to define one in `YAML`. 

This manifest creates a pod with a single container that runs the `myapp` image on port 80.

```yml
apiVersion: v1
kind: Pod
metadata:
  name: myapp
spec:
  containers:
  - name: mycontainer
    image: myapp:latest
    ports:
    - containerPort: 80
```

### Deploying a Multi-Container Application

To deploy a multi-container application, create a `manifest` that defines a pod with multiple containers.

```yml
apiVersion: v1
kind: Pod
metadata:
  name: myapp
spec:
  containers:
  - name: mycontainer1
    image: myapp:latest
    ports:
    - containerPort: 80
  - name: mycontainer2
    image: myapp2:latest
```

### Scaling an Application

To scale an application, you can define how many HA deployments you would want by specifying the `replicas` in your `yml` file.

Here's an example deployment file for a Node.js application with `3` replicas:

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-app
        image: my-app-image:latest
        ports:
        - containerPort: 3000
```

### Apply

Apply the deployment by running the following command:

```bash
kubectl apply -f deployment.yaml
```

This command creates the deployment and replicas in your cluster.

Kubernetes provides a stable IP address and DNS name for accessing your application. 

It can also load balance traffic between replicas of your application.

## Conclusion

Kubernetes is a powerful platform for deploying, scaling, and managing containerized applications. 

With its many components and features, it can seem daunting at first, but once you get started, you'll find that it's a valuable tool for building and managing complex distributed systems. 

By following the examples above and exploring the many resources available online, you can quickly become proficient in using Kubernetes to deploy and manage your applications.

### Note

Be aware, products can change over time. I do my best to keep up with the latest changes and releases. The documentation above may become outdated or inaccurate. 

Always refer to the latest official documentation and resources.

### Learn More

- [Official Documentation](https://kubernetes.io/docs/home/)
- [Kubernetes Components](https://kubernetes.io/docs/concepts/overview/components/)
- [Minikube Start](https://minikube.sigs.k8s.io/docs/start/)
- [Minikube Tutorial](https://kubernetes.io/docs/tutorials/hello-minikube/)
- [Kubernetes Lab by Tutorius](https://labs.play-with-k8s.com/)
- [Workshop by Docker](https://training.play-with-kubernetes.com/kubernetes-workshop/)
- [Additional Resources](https://docs.google.com/spreadsheets/d/10NltoF_6y3mBwUzQ4bcQLQfCE1BWSgUDcJXy-Qp2JEU/edit#gid=0)