# Deployment View 

The Deployment view focuses on aspects of the system that are important after the system has been tested and is ready to go into live operation. This view defines the physical environment in which the system is intended to run, including the hardware environment your system needs (e.g., processing nodes, network interconnections, and disk storage facilities), the technical environment requirements for each node (or node type) in the system, and the mapping of your software elements to the runtime environment that will execute them

The main concerns are: Types of hardware required, specification and quantity of hardware required, third-party software requirements, technology compatibility, network requirements, network capacity required, and physical constraints


## Components 
### Networking
The goal of this document is to allow the reader to understand the design of the _VPC_. A _VPC_ is akin to a network infrastructure setup that you could be familiar with from on-premise ecosystems. 

Read the full document [here](infrastructure/InfrastructureAndNetworking.md).

### Scaling and balancing
To be as performant and cost-effective as possible we have adopted a strategy where we don't scale up but scale-out. An example of scaling up would be upgrading a server to better (virtual) hardware so the workload can be handled. In a scale-out scenario, the heavy workload would be handled by multiple instances of the server.

![Figure 1: Scaling strategies](/img/scaling-strategies.png)

Figure 1: Scaling strategies

### (Virtual) hardware and services
A full overview of all the (virtual) hardware and services used can be found [here](infrastructure/Infrastructure-services-and-virtual-hardware.md). 

### Authentication
Authentication allows us to check the identity of a user or (external) system. We also use authentication to allow us to store some personal information of a user securely.

Read the full document [here](infrastructure/Authentication.md).

## Risks 
1. OpenStreet Maps have a fair-use license. As such, there is always a risk that the service is either unavailable or somewhat outdated. (See: [ADR 015](/4.ADRs/015%20Integration%20with%20Map%20Providers.md)))

*Risk reduction:* Aside from switching providers, there is also the possibility of caching the tilemaps and internalizing the location data.

## Cost analysis
The cost analysis can be found [here](CostAnalysis.md)

## Glossary of abbreviations
Here we will introduce some terms that are used in the infrastructure documentation.

AMQ: Amazon MQ (Manages message queue service)

ASG: Auto-scaling group

AWS: Amazon Web Service

EC2: Elastic Compute Cloud

S3: Simple Storage Service

VPC: Virtual Private Cloud

VPG: Virtual Private Gateway


CAPEX: Capital expenses
OPEX: Operational expenses


CIDR: Classless Inter-Domain Routing

DataDog: See [DataDog](/4.ADRs/003%20Tracing%20and%20Monitoring%20Sytem.md)

JSON: JavaScript Object Notation

JWT: JSON Web Token

SaaS: Software as a Service

SMS: Short Message Service

REST: Representational state transfer

VPN: Virtual Private Network

## Checklist 

* Have you mapped all of the system’s functional elements to a type of hardware device? 
* Have you mapped them to specific hardware devices if appropriate?
* Is the role of each hardware element in the system fully understood? 
* Is the specified hardware suitable for the role?
* Have you established detailed specifications for the system’s hardware devices? Do you know exactly how many of each device are required?
* Have you identified all required third-party software and documented all the dependencies between system elements and third-party software?
* Is the network topology required by the system understood and documented?
* Have you estimated and validated the required network capacity? 
* Can the proposed network topology be built to support this capacity?
* Have network specialists validated that the required network can be built?
* Have you performed compatibility testing when evaluating your architectural options to ensure that the elements of the proposed deployment environment can be combined as desired?
* Have you used enough prototypes, benchmarks, and other practical tests when evaluating your architectural options to validate the critical aspects of the proposed deployment environment?
* Can you create a realistic test environment that is representative of the proposed deployment environment?
* Are you confident that the deployment environment will work as designed?
* Have you obtained an external review to validate this opinion?
* Are the assessors satisfied that the deployment environment meets their requirements in terms of standards, risks, and costs?
* Have you checked that the physical constraints (such as floor space, power, cooling, and so on) implied by your required deployment environment can be met?
