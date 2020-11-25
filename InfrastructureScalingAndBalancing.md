# Infrastructure scaling and load balancing

## Auto scaling
![Auto scaling](/img/infra-auto-scaling.png)
Figure 1: Auto scaling

Auto scaling is applied to all _Elastic Cloud Compute_ (_EC2_) instances in the public subnets. This takes care of scaling for us based on certain load criteria.

The default setting recommendation for the auto scaling groups is:  **Balance availability and cost**. Furthermore, by default only _EC2_ instances should be part of the auto-scaling group. However, if needed other resources can be configured to be added to the group.

## Metric based scaling
At this point in the project it is unknown what metric would best serve Farmacy Foods' best interests. At this point we would advise:
- CPU utilization > 75%
- Memory utilization > 90%

Metric reporting is crucial to guide your choice of scaling options.

## Load Balancing

![Balancing overview](/img/Balancing-Overview.png)
Figure 2: Load balancing

### Route 53 DNS

Amazon Route 53 is a highly available and scalable cloud Domain Name System (DNS) web service. [...] Amazon Route 53 effectively connects user requests to infrastructure running in AWS – such as Amazon EC2 instances, Elastic Load Balancing load balancers, or Amazon S3 buckets – and can also be used to route users to infrastructure outside of AWS. You can use Amazon Route 53 to configure DNS health checks to route traffic to healthy endpoints or to independently monitor the health of your application and its endpoints.[1](#references)

### Application Load Balancer (_ALB_)

The _Application Load Balancer_ provided by _AWS_ is responsible for distributing traffic among our internet facing services and _EC2_ instances. For some services we do this indirectly by using the _Auto Scaling Group_. The _ALB_ is a request level load balancer. ([Layer 7](https://en.wikipedia.org/wiki/Application_layer))

Using the ALB allows us to balance on the basis of an application interface. In our case this mostly means that we can have, REST API, resource bound load balancing. This is includes application specific resources but also resources on the authentication api provided by Cognito. (See: [Authentication](/Authentication.md))

> In Figure 2 we see two rules in the ruleset:
> 1. Redirect http to https.
> 2. /X
>
> The first rule is responsible for redirecting http based traffic to https. In essence, this stops the use of http.
> The second rule is a placeholder to forward requests to /X to a certain endpoint (for instance an _Auto Scaling Group_ or and resource on the Cognito API.

Another advantage of the _ALB_ is the native ability to force HTTPS connections only. We do this by making use of a configurable rule in the rulesets of the loadbalancer.

### AWS Certificate Manager (_ACM_)

The AWS Certificate Manager is used to store [TLS](https://en.wikipedia.org/wiki/Transport_Layer_Security) certificates. In our case this we use ACM to store both [Certificate Authority](https://en.wikipedia.org/wiki/Certificate_authority) acknowledged certificates and private certificates. The latter are used for development and test environments.

### Listener
A listener is a process that checks for connection requests, using the protocol and port that you configured. You can configure HTTP or HTTPS on the standard port but you could also add additional listeners on non-standard ports.

### Ruleset
Rulesets are attached to an _ALB_ and contain rules that can be used to perform specific _Actions_ on incomming requests. We use this to:
- redirect an **non-authenticated** user to Cognito for authentication.
- check a JWT against Cognito to verify correct authentication of the user. (Redirecting the user when the JWT is not valid.)
- forward traffic to the scaling group based on the requested resource path.

### Target group
We use _target groups_ to point to the actual resource behind the _ALB_. For instance, our _ASG_, an _EC2_ instance or any other kind of service resource that we want to be internet-facing.

### References
1: https://aws.amazon.com/route53/
