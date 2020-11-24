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
Private subnets are designed for internal IP addresses. They are typically not reachable from the broader internet and are bound to strict egress rules. 

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

## Auto scaling
![Auto scaling](/img/infra-auto-scaling.png)

Auto scaling is applied to all Elastic Cloud Compute (EC2) instances in the public subnets. This takes care of scaling for us based on certain load criteria.

The default setting recommendation for the auto scaling groups is:  **Balance availability and cost**. Furthermore, by default only EC2 instances should be part of the auto-scaling group. However, if needed other resources can be configured to be added to the group.


