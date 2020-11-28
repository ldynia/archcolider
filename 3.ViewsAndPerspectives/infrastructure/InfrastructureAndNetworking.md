# Infrastructure and networking

## VPC design

![VPC Design](/img/infra-vpc.png)

### Availability zone and Region
An _Availability Zone_ (_AZ_) is one or more discrete data centers with redundant power, networking, and connectivity in an _AWS Region_. 

We have elected to design the infrastructure using two availability zones that are within a single _AWS region_. The choice for the region us-east was based on the location of the client and its proximity to the region's data center.

For more information on Regions and Availability Zones, see https://aws.amazon.com/about-aws/global-infrastructure/regions_az/

### Subnets
Subnets are simply parts of a network. These subnets are assigned a range of Internet Protocol (IP) addresses using a notation known as _CIDR_ blocks. Any address within such an assigned _CIDR_ block is said to be in the subnet the _CIDR_ block belongs to.

> Note: Only IPv4 is considered for both the design and this document.

#### Public subnet
Public subnets are designed for externally available IP addresses. They tend to be reachable from the broader internet and are allowed egress. (Restriction may apply) In our specific case we will allow secure traffic from the internet on predefined API resources.

#### Private subnet
Private subnets are designed for internal IP addresses. They are typically not reachable from the broader internet and are bound to strict egress rules. The IP addresses in the private subnet are accessible from VPN connected elements. You can restrict this in route tables for the private subnets.

We will not allow any traffic from the internet directly on our private subnets.

### Route tables
Route tables allow you to dictate the flow of network traffic.

> The concept of a private or public subnet is an abstract one. You will not find an AWS resources named as such. The rout table determines if a subnet is private or public.

Route tables should be read from Destination to Target. Meaning, when an element within a subnet tries to reach a target IP address it will go to the route table to see if/how it can get there. For example, if a route table states the Destination as 0.0.0.0/0 with Target igw-1 it means that in order to go to any IP address it should go through internet gateway-1. The astute reader can conclude that such a rule should not be at the top of the table as the table will be in order of priority. (Exceptions may apply in some scenarios)

> 0.0.0.0/0 in _AWS_ means ANY ip4 address. 

Below you will find the minimal route tables needed for our infrastructure design.

#### Route table for public subnets
| Destination      | Target   | Comment             |
| ----        | ------        | ------              |
| 10.0.0.0/16 | Local         | Allows for traffic between local elements |
| 0.0.0.0/0   | igw-1         | Allow internet traffic |

#### Route table for private subnets

| Destination      | Target   | Comment             |
| ----        | ------        | ------              |
| 10.0.0.0/16 | Local         | Allows for traffic between local elements |

The lack of connection to the internet for the private subnets is intentional as no service running there should be accessible through the internet directly.

#### Internet Gateway
The _Internet Gateway_ (in the diagram named **igw-1**) is used to allow your route table to point to it for internet routable traffic. It also performs network address translation (NAT) for instances that have a public IP address assigned.

### Amazon Virtual Private Network
Any on-premise system that's already in use can be connected to systems within the _VPC_ using a secure _VPN_ connection. Please note, there is no need to go through the _VPN_ for public actions such as requesting a publicly available _REST_ endpoint on an _API_. Prefer such a public end-point when they are available.

The _VPN_ will connect to a _VPC_ requiring the route table to be set in such a way that communication between the on-premise network and the _VPC_ is possible.

> #### Example
> Using an on-premise network with _CIDR_ block 192.168.0.0/16 and a _VPC_ with _CIDR_ block 10.0.0.0/16 you would need the following route table entry:
> | Destination | Target |
> | --- | --- |
> | 192.168.0.0/0 | VGW |
>
> This example shows only the entry needed to connect to the _Virtual Private Gateway_. Other entries are not shown.

## Evolutionary perspective
In this paragraph, we try to show how a select number of scenarios would be handled if they occur in the future. This document only discusses network related items. For more on scaling see: [Infrastructure scaling and balancing](InfrastructureScalingAndBalancing.md)

### Increase up-time
**The trade-off:** Increasing theoretical up-time will require an increase in budget.
To increase up-time we could add an availability zone. For instance, adding us-east-2c, will add an additional one. Should you run up against the limit of availability zones for your infrastructure, you could always add a _Region_. _VPCs_ can contain multiple _Availability Zones_ however, you cannot span a _VPC_ over multiple _AWS regions_. Depending on the way you scale you may need to add _VPC_ peering in order to fluently work with other VPCs. See: [VPC Peering](https://docs.aws.amazon.com/vpc/latest/peering/what-is-vpc-peering.html)

### General decrease in load
**The trade-off:** Cost will decrease but theoretical up-time will decrease.
Should you have multiple VPCs connected by a _VPC_ Peering Connection you should consider removing that first as it weighs more heavily on the budget than _AZs_ do. Removing and _AZ_ completely (and thus all its resources within) you could cut cost and get nearer to the actual load requirements.

### Adding new service areas (locations far outside of Detroit)
**The trade-off:** Costs increase due to infrastructure replication which in turn allows you to have the infrastructure closer to the customers.
Using edge locations or new _AWS regions_ you can move your infrastructure and operations closer to the customer. This will likely increase the speed of operations.

A _CDN_ can be introduced if there is a need for quicker delivery of static content.

### Removing new service areas
**The trade-off:** Costs decrease due to infrastructure removal which in turn may affect operations speed negatively.
Terminating a service area that has no other areas that could benefit from having edge locations or _AWS regions_ close to them should lead you to consider terminating them.

> **Important:** At first glance it may seem very natural to add a new _AWS region_ or edge location when adding a new service area. However, consider that you should only take this course of action when operations slow down in such a way that it has a major negative impact on the customer or other stakeholder. The customer or other stakeholders should represent the monetary value of the cost of the extra infrastructure and other _OPEX_.
