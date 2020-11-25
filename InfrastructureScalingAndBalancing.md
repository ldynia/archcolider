# Infrastructure scaling and load balancing

## Auto scaling
![Auto scaling](/img/infra-auto-scaling.png)

Auto scaling is applied to all _Elastic Cloud Compute_ (_EC2_) instances in the public subnets. This takes care of scaling for us based on certain load criteria.

The default setting recommendation for the auto scaling groups is:  **Balance availability and cost**. Furthermore, by default only _EC2_ instances should be part of the auto-scaling group. However, if needed other resources can be configured to be added to the group.

## Metric based scaling
At this point in the project it is unknown what metric would best serve Farmacy Foods' best interests. At this point we would advise:
- CPU utilization > 75%
- Memory utilization > 90%

Metric reporting is crucial to guide your choice of scaling options.

## Load Balancing

![Balancing overview](/img/Balancing-Overview.png)

### Route 53 DNS

Amazon Route 53 is a highly available and scalable cloud Domain Name System (DNS) web service. [...] Amazon Route 53 effectively connects user requests to infrastructure running in AWS – such as Amazon EC2 instances, Elastic Load Balancing load balancers, or Amazon S3 buckets – and can also be used to route users to infrastructure outside of AWS. You can use Amazon Route 53 to configure DNS health checks to route traffic to healthy endpoints or to independently monitor the health of your application and its endpoints.[1](#references)


### Application Load Balancer (_ALB_)

### AWS Certificate Manager (_ACM_)

### Listener

### Ruleset

### Target group

### References
1: https://aws.amazon.com/route53/
