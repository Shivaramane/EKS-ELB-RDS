This repo contains manifests about the below:

EKS-ALB-RDS: This contains manifests about using EKS through ALB to access the Frontend application and uses NodePort Service to access the backend MySQL RDS DB.

EKS-CLB-RDS: This is the demonstrate how to use ClassicLoadBalancer to expose Service deployed in Public subnets and MySQL RDS available in Private Subnet.

EKS-Storage-EBS: This section uses EBS CSI Driver and use EBS Volumes for persistence storage to MySQL Database.

EKS-Storage-RDS: This section utilises RDS MySQL Database on AWS EKS Cluster.

External-DNS-EKS: This contains manifests about using EKS through ALB to access the Frontend application and uses NodePort Service to access the backend MySQL RDS DB.
This also uses implements SSL using ACM, HTTP to HTTPS redirect, ExternalDNS to register the domain names in Route53.

YAML-examples: YAML manifest to implement ClusterIP, NodePort Service, fronend deployment, backend deployment etc.






