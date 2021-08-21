Features included:

********ALB Ingress Controller Path based routing**************

********AWS ALB Ingress Controller - Implementation of HTTP to HTTPS Redirect************

********External DNS - Used for Updating Route53 RecordSets from Kubernetes**************

**Steps for ALB Ingress Controller installation:**

1. Create and associate IAM OIDC provider for EKS Cluster.

2. Create Service Account with Cluster Role & Cluster Role Binding using the below rbac-role.yaml

https://raw.githubusercontent.com/kubernetes-sigs/aws-alb-ingress-controller/master/docs/examples/rbac-role.yaml

3. Create an IAM Policy which will allow our ALB Ingress Controller pod to make calls to AWS API's.
Use the below policy.

https://raw.githubusercontent.com/kubernetes-sigs/aws-alb-ingress-controller/master/docs/examples/iam-policy.json

4. Create an IAM role for the ALB Ingress Controller and attach the role to the service account. This can be performed only on EKS managed cluster. This will create an IAM Role and bounds that role to K8S Service account.

5. Deploy the Ingress Controller Manifest and verify the ALB Ingress Controller pod is running.



**Steps for ALB Ingress Controller SSL enabling**

1. Using ACM request a certificate of type Public.
2. Add the domain names as *.urdomain.com (in my case it is hellosample.net)
3. Add the below annotations to the ALB Ingress manifest for enabling SSL.

alb.ingress.kubernetes.io/listen-ports: '[{"HTTPS":443}, {"HTTP":80}]'
alb.ingress.kubernetes.io/certificate-arn: arn:aws:acm:us-east-1:your-certificate-arn

4. Select Validation method as DNS Validation and this creates CNAME record of the certificate in the hosted zone.

**Steps for ALB Ingress Controller HTTP to HTTPS redirect**

This is achieved using Custom Action Annotation.

This annotation provides a method for configuring custom actions on a listener, such as for Redirect Actions.

The action-name in the annotation must match the serviceName in the ingress rules, and servicePort must be use-annotation.

alb.ingress.kubernetes.io/actions.ssl-redirect: '{"Type": "redirect", "RedirectConfig": { "Protocol": "HTTPS", "Port": "443", "StatusCode": "HTTP_301"}}'   

**Steps for implementing External DNS**

External DNS is used for Updating Route53 RecordSets from Kubernetes

1. Create Service Account with Cluster Role & Cluster Role Binding using the below manifest for clusters with RBAC enabled.

https://github.com/kubernetes-sigs/external-dns/blob/master/docs/tutorials/aws.md

2. Create an IAM Policy which will allow external-dns pod to add, remove DNS entries (Record Sets in a Hosted Zone) in AWS Route53 service.

3. Create an IAM role for the External DNS and attach the role to the service account. This can be performed only on EKS managed cluster. This will create an IAM Role and bounds that role to K8S Service account.

4. Update Ingress manifest by adding External DNS Annotation

# External DNS - For creating a Record Set in Route53
    external-dns.alpha.kubernetes.io/hostname: dnstest1.hellosample.net, dnstest2.hellosample.net    
5. Deploy the manifests.

*********This also has httpd-backend deployment which is used to resolve the error "endpoints “default-http-backend” not found in Ingress resource"************

