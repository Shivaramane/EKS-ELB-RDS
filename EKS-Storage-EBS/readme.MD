
**This section uses EBS CSI Driver and use EBS Volumes for persistence storage to MySQL Database.**

EBS CSI Driver is a K8S obj which runs in kube-system.

This also utilises K8S features such as Request and Limits. Below are the features of this obj.

** Can specify how much each container a pod needs the resources like CPU & Memory.

** When this information given to our pod, the scheduler uses this information to decide which node to place the Pod on.

** When resource limit for a Container is specified, the kubelet enforces those limits so that the running container is not allowed to use more of that resource than the limit you set.

** The also ensures the kubelet to reserve at least the request amount of that system resource specifically for that container to use.
