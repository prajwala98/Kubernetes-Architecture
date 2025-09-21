# Kubernetes-Architecture
Kubernetes Cluster has two components, DATA PLANE and CONTROL PLANE.

DATA PLANE/worker node:

1.KUBELET-Ensures that Pods are running, including their containers.

2.KUBE-PROXY-Maintains network rules on nodes to implement Services.

3.CONTAINER RUNTINE-Software respomsible for running containers.

CONTROL PLANE:

1.KUBE-APISERVER-The core component server that exposes the Kubernetes HTTP API.

2.ETCD-Consistent and highly-available key value store for all API server data.

3.KUBE-SCHEDULER-Looks for Pods not yet bound to a node, and assigns each Pod to a suitable node.

4.KUBE-CONTROLLER-MANAGER-Runs controllers to implement Kubernetes API behavior.

5.CLOUD-CONTROLLER-MANAGER-Integrates with underlying cloud provider(s).


let us understand Kubernetes Architecture in comparision with docker- On virtual machine,as a user we have installed docker. To run a container we have a container runtime component called as Dockershim. Kubernetes also provides with similar behaviour but with advanced enterprise level support with AUTO-SCALING, AUTO-HEALING and CLUSTER like features. We deploy CONTAINER in docker,whereas the smallest level of deployment in kubernetes is a POD on a specific WORKER NODE.

KUBELET,a component of worker node, ensures that Pods are running, including their containers.If our pod is not running,then Kubelet informs about the issue to one of the components in Control plane. In Kubernetes our request first passes through control plane before reaching data plane/worker node.As docker has docker engine and dockershim to run its containers, kubernetes has KUBELET with Auto-healing feature to keep the pod up amd running.

Docker has only Dockershim for its container runtime but Kubernetes supports several container runtimes including CRI-O, CONTAINERD, DOCKER ENGINE or any other such software that meets the standards kubernetes has set.You need to install a container runtime into each node in the cluster so that Pods can run.

KUBE-PROXY provides networking,IP Address generation for ur pods and provides with load-balncing capabilities. Kube-proxy uses iptables for networking related configuration.Using the above 3 components kubelet,kube-proxy anc container runtime, we can technically have everything to run our application. Yet we need Control plane/Master component for Kubernetes because of some specific standards such as a CLUSTER.

For ex: A use has created a pod, there should be a mechanism that decides whether the pod is to be created on node1 or node2. When multiple users are trying to access kubernetes cluster (or) implement identity provider for configuring SSO, there has to be core component as heart of kubernetes that deals with all instructions.

KUBE-APISERVER exposes Kubernetes to external world and acts on the information provided. A user creating a pod actually tries to access API SERVER  and from here kubernetes decided which node is free. But to schedule a pod to a node , we have a component called KUBE-SCHEDULER that schedules resources on Kubernetes.

A critical component in Kubernetes that acts as a primary backupstore of entire cluster information is ETCD. Data is stored as objects or key value pairs inside this centralised data store.

Kubernetes supports AUTO-SCALING and to enable this feature Kubernetes has some controllers such as Replica sets.The component that runs controllers is KUBE-CONTROLLER-MANAGER. For ex: In kubernetes yaml file the mentioned number of replica sets are always running by replica set controller.

If Kubernetes has to create a load balancer on AWS , Kubernetes translates the request from the user to the API request that AWS understands. This mechanism is implemented by CLOUD-CONTROLLER-MANAGER. CCM is an open source utility that enables us to write cloud-specific logic,enabling faster development and deployment of features by cloud providers without needing to modify the main kubernetes project.The cloud controller manager lets us link our cluster into the specific cloud provider's API, and separates out the components that interact with that cloud platform from components that only interact with our cluster.The cloud-controller-manager is structured using a plugin mechanism that allows different cloud providers to integrate their platforms with Kubernetes. But if we are running kubernetes on on-premises cloud , this component is not required.
Therefore the control plane/master has controlling actions whereas,  the data plane/ worker is internal and has executing actions.

We have plethora of information on kubernetes architecture on the internet but thus write-up includes a bit of my understaning on this topic.
