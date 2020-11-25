# Deployment strategy

Date: 2020-11-20

## Status

Proposed

## Context

Once the solution is implemented it has to be cheap to deploy, maintain and scale. Currently there are several options that we could take into consideration as a deployment platforms such: on premise servers, serverless solutions, container orchestrations such as Kubernetes (on premise or as PaaS), or OpenShift -enterprise flavour of on premise Kubernetes. Finally, we could choose to use virtual servers provided by AWS or Azure.

## Decision

We decided to go with virtual machines (EC2 instances) on AWS for two reasons. First, we can start with minimum instances and decide to scale up (scale vertically) on CPU and Memory. When we will reach limits of up scaling then  natural thing  to follow is,  to scale out (scale horizontally) increasing the number of running instances. Second, Horizontal scaling adhere to our architecture where we can scale individual components of our system according to component's load. Another decision behind dropping popular solutions such Kubernetes, is the effort of work that needs to be invested into the platform, starting from learning Kubernetes ending on provisioning Kubernetes cluster with monitoring, metrics and inter-service networking such service mesh.


## Consequences

Using micro EC2 instances will keep costs low. Morover, we will use containers (Docker or similar) for application development and put them behind reverse proxy. 

**Positive:** Low cost, Low cognitive footprint, Easy maintenance

**Negative:** Vendor lock-in

**Risks:** 
