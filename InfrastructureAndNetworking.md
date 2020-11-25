# Infrastructure and networking
The goal of this document is to allow the reader to understand the design of the AWS VPC. (Amazon's Virtual Private Cloud) A VPC is akin to a network infrastructure setup that you could be familiar with from on-premise ecosystems.

## VPC design

![VPC Design](/img/infra-vpc.png)

### Availability zone and Region
An Availability Zone (AZ) is one or more discrete data centers with redundant power, networking, and connectivity in an AWS Region. 


We have elected to design the infrastructure using two availability zones that are within a single Region. The choice for the region _us-east_ was based on the location of the client and its proximity to the region's data center.

For more information on Regions and Availability Zones, see https://aws.amazon.com/about-aws/global-infrastructure/regions_az/

### Subnets
Subnets are simply parts of a network. These subnets are assigned a range of Internet Protocol (IP) addresses using a notation know as Classless Inter-Domain Routing (CIDR) blocks. Any address within such an assigned CIDR block is said to be in the subnet the CIDR block belongs to.

> Note: Only IPv4 is considered for both the design and this document.

#### Private subnet
Public subnets are designed for externally available IP addresses. They tend to be reachable from the broader internet and are allowed egress. (Restriction may apply)

#### Private subnet
Private subnets are designed for internal IP addresses. They are typically not reachable from the broader internet and are bound to strict egress rules. The IP addresses in the private subnet are accessible from VPN connected elements. You can restrict this in route tables for the private subnets.

### Route tables
Route tables allow you to dictate the flow of network traffic much like you may be used to from a home router.

Route tables should be read from Destination to Target. Meaning, when a element within a subnet tries to reach a target ip address it will go to the route table to see if/how it
can get there. For example, if a route table states the Destination as 0.0.0.0/0 with Target igw-1 it means that in order to go to any ip address it should go through internet gateway-1. The astute reader can conclude that such a rule should not be at the top of the table as the table will be in order of priority. (Exceptions may apply in some scenarios)

> 0.0.0.0/0 in AWS means ANY ip4 address. 

#### Route table for public subnets
| Destination      | Target   | Comment             |
| ----        | ------        | ------              |
| 10.0.0.0/16 | Local         | Allows for traffic between local elements |
| 0.0.0.0/0   | igw-1         | Allow internet traffic |

#### Route table for private subnets

| Destination      | Target   | Comment             |
| ----        | ------        | ------              |
| 10.0.0.0/16 | Local         | Allows for traffic between local elements |

The lack of connection to the internet for the private subnets is intentional as no service running there should be accessable through the internet directly.

#### Internet Gateway
The Internet Gateway (in the diagram named **igw-1**) is used to allow your route table to point to it for internet routable traffic. It also performs network address translation (NAT) for instances that have public IP address assigned.

### Amazon Virtual Private Network
Any on-premise system that's already in use can be connected to systems within the VPC using a secure virtual private network (VPN) connection. Please note, there is no need to go through the VPN for public actions such as requesting a publicly available REST endpoint on an API. Prefer such public end-point when they are available.

The VPN will connect to a VPC requiring the route table to be set in such a way that communication between the on-premise network and the VPC is possible.

> #### Example
> Using an on-premise network with CIDR block 192.168.0.0/16 and a VPC with CIDR block 10.0.0.0/16 you would need the following route table entry:
> | Destination | Target |
> | --- | --- |
> | 192.168.0.0/0 | VGW |
>
> This example shows only the entry needed to connect to the Virtual Private Gateway. Other entries are not shown.

## Evolutionary perspective
In this paragraph we try to show how a select number of scenarios would be handled if they occur in the future. This document only discusses network related items. For more on scaling see: [Infrastructure scaling and balancing](InfrastructureScalingAndBalancing.md)

### Increase up-time
**The trade-off:** Increasing theoretical up-time will require an increase in budget.
To increase up-time we could add an availability zone. For instance, adding _us-east-2c_, will add an additional one. Should you run up against the limit of availability zones for your infrastructure, you could always add a _Region_. VPCs can contain multiple _Availability Zones_ however, you cannot span a VPC over multiple regions. Depending on the way you scale you may need to add VPC peering in order to fluently work with other VPCs. See: [VPC Peering] (https://docs.aws.amazon.com/vpc/latest/peering/what-is-vpc-peering.html)

### General decrease in load
**The trade-off:** Cost will decrease but theoretical up-time will decrease.
Should you have multiple VPCs connected by a _VPC Peering Connection_ you should consider removing that first as it weighs more heavily on the budget than _AZs_ do. Removing and _AZ_ completely (and thus all its resources within) you could cut cost and get nearer to the actual load requirements.

### Adding new service areas (locations far outside of Detroit)
**The trade-off:** Costs increase due to infrastructure replication which in turn allows you to have the infrastructure closer to the customers.
Using _edge locations_ or new _regions_ you can move your infrastructure and operations closer to the customer. This will likely increase the speed of operations.

A CDN can be introduced if there is a need for quicker delivery of static content.

### Removing new service areas
**The trade-off:** Costs decrease due to infrastructure removal which in turn may affect operations speed negatively.
Terminating a serive area that has no other areas that could benefit from having _edge locations_ or _regions_ close to them should lead you to consider terminating them.

> Important: At first glance it may seem very natural to add a new _region_ or _edge location_ when adding a new service area. However, consider that you should only take this course of action when operations slow down in such a way that it has a major negative impact on the customer or other stakeholder. The customer or other stakeholders should represent the monetary value of the cost of the extra infrastructure and other OPEX.
