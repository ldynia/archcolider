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

### Application Load Balancer (_ALB_)

### AWS Certificate Manager (_ACM_)

### Listener

### Ruleset

### Target group
