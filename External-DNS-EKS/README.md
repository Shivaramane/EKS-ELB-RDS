Features included:

********External DNS - Used for Updating Route53 RecordSets from Kubernetes**************

********AWS ALB Ingress Controller - Implementation of HTTP to HTTPS Redirect************
Provides a method for configuring custom actions on a listener, such as for Redirect Actions.
The action-name in the annotation must match the serviceName in the ingress rules, and servicePort must be use-annotation.
This is achieved using Custom Action Annotation


*********This also has httpd-backend deployment which is used to resolve the error "endpoints “default-http-backend” not found in Ingress resource"************

