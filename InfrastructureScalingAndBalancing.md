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

Amazon Route 53 is a highly available and scalable cloud Domain Name System (DNS) web service. (*) It is designed to give developers and businesses an extremely reliable and cost effective way to route end users to Internet applications by translating names like www.example.com into the numeric IP addresses like 192.0.2.1 that computers use to connect to each other. Amazon Route 53 is fully compliant with IPv6 as well.

Amazon Route 53 effectively connects user requests to infrastructure running in AWS – such as Amazon EC2 instances, Elastic Load Balancing load balancers, or Amazon S3 buckets – and can also be used to route users to infrastructure outside of AWS. You can use Amazon Route 53 to configure DNS health checks to route traffic to healthy endpoints or to independently monitor the health of your application and its endpoints. Amazon Route 53 Traffic Flow makes it easy for you to manage traffic globally through a variety of routing types, including Latency Based Routing, Geo DNS, Geoproximity, and Weighted Round Robin—all of which can be combined with DNS Failover in order to enable a variety of low-latency, fault-tolerant architectures. Using Amazon Route 53 Traffic Flow’s simple visual editor, you can easily manage how your end-users are routed to your application’s endpoints—whether in a single AWS region or distributed around the globe. Amazon Route 53 also offers Domain Name Registration – you can purchase and manage domain names such as example.com and Amazon Route 53 will automatically configure DNS settings for your domains.[1](#references)


### Application Load Balancer (_ALB_)

### AWS Certificate Manager (_ACM_)

### Listener

### Ruleset

### Target group

### References
[1]: https://aws.amazon.com/route53/
