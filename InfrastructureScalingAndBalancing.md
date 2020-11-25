# Infrastructure scaling and balancing

## Auto scaling
![Auto scaling](/img/infra-auto-scaling.png)

Auto scaling is applied to all Elastic Cloud Compute (EC2) instances in the public subnets. This takes care of scaling for us based on certain load criteria.

The default setting recommendation for the auto scaling groups is:  **Balance availability and cost**. Furthermore, by default only EC2 instances should be part of the auto-scaling group. However, if needed other resources can be configured to be added to the group.
