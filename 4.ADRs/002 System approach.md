# System approach

Date: 2020-10-29

## Status

Accepted 

## Context

We need to decide what is the dominating system approach will be. There are several option like: monolith, microservices, micro-kernels, blackboard. 

There are also technical constraints and business drivers even if sky is blue and we are free of choice, developer's team experience and capabilities should be considered. 

### Alternatives 

Key map: 
- + Promotes
- ++ Strongly promotes 
- O Neutral 
- - Negative 
- -- Strongly negative

| | Monolith | Microservices | Micro-kernel |
|----|----|----|-----|
| Ease of Deployment  | ++ | -  | -  | 
| Availability        | -  | ++ | +  |
| Autonomity          | -- | ++ | ++ | 
| Traceability        | ++ | -  | +  | 
| Performance         | ++ | +  | +  | 
| Modifability        | O  | ++ | +  | 
| Maintanability      | -  | ++ | +  | 
| Integrity           | ++ | -- | O  | 
| Security            | -  | ++ | +  | 
| Scalability         | -- | ++ | -  | 
 
## Decision

Based on alternatives in the context of the business needs and a development team we think that micro-kernel approach is the best option for now. At the same time it opens possibility to migrate to microservices when needed. 

Can be converted to highly modularized monolith with characteristics of micro-kernel approach

## Consequences

The major parts of the system will requires careful API management to make possible unified access to the kernel. At the same time it gives solid base for the development and tracking what should be converted to microservices. 

Micro-kernels requires more attentions from developers, but still allows independent development of major parts and extend main functionality with 3rd party plug-ins. 
