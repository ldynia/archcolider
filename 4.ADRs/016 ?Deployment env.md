# Record architecture decisions

Date: 2020-11-20

## Status

Proposed

## Context

Once the solution is implemented it has to be cheap to deploy, maintain and scale. Currently there are several options that we could take into consideration as a deployment platforms such: on premise servers, serverless solutions, container orchestrations such as Kubernetes (on premise or as PaaS), or OpenShift -enterprise flavour of on premise Kubernetes. Finally, we could choose to use virtual servers built from EC2 instances.

## Decision

We decided to go with EC2 instances for two reasons. First, we can start with minimum instances and decide to scale up / scale vertically on CPU and Memory.
When we will reach limits of up scaling then the natural thing to follow is to scale out / scale horizontally increasing the number of instance running the applicatio. Another decision behind dropping popular solutions such Kubernetes, is the effort of work that needs to be invested into platform starting from learning ending on profisioning kubernetes cluster with monitoring, metrics and inter-service networking such service mesh.


## Consequences

Using EC2 virtual machines will keep costs low. Morover, we will use containers (Docker or similar) for application development and put them behind reverse proxy. 

**Positive:** Low cost, Low cognitive footprint, Easy maintenance

**Negative:**

**Risks:** Vendor lock-in

**Bonus Features:**
