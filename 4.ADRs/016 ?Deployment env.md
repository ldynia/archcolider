# Record architecture decisions

Date: 2020-11-20

## Status

Proposed

## Context

Once solutions are implemented it has to be deployed in a way that is easy to maintain, learn (cognitive aspect of development), scale and finally is cost effective.
Currently there are several options that we could take into consideration such: on premise servers, serverless solutions, container orchestrations such Kubernetes
which could be deployed on premise or used as PaaS, or OpenShift enterprise flavour of Kubernetes. Finally, we could choose to use virtual servers built from EC2 instances.

## Decision

We decided to go with EC2 instances for two reasons. First, we can start with minimum instances and decide to scale up / scale vertically on CPU and Memory.
When we will reach limits of up scaling then the natural thing to follow is to scale out / scale horizontally increasing the number of instances.
Another decision behind dropping popular solutions such Kubernetes is the effort of work that needs to be invested into platform starting from learning ending on
installing tool responsible for monitoring, metrics and inter service networking such service mesh.    

## Consequences

Using EC2 virtual machines will keep costs law. We can still use containers (Docker or similar) for application development and put them behind reverse proxy in production.


**Positive:** Low cost, Low cognitive footprint, Easy maintenance

**Negative:**

**Risks:** Vendor lock-in

**Bonus Features:**
