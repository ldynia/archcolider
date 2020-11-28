# System approach

Date: 2020-10-29

## Status

Accepted

## Context

We need to decide what the dominating system approach will be. There are several options like: monolith, microservices, micro-kernels, blackboard.

There are also technical constraints and business drivers even if the sky is blue and we are free of choice, developer's team experience and capabilities should be considered.

### Alternatives

Key map:
- + Promotes
- ++ Strongly promotes
- O Neutral
- - Negative
- -- Strongly negative

| | Monolith | Microservices | Micro-kernel | Modularized Monolith |
|----|----|----|-----|-----|
| Ease of Deployment  | ++ | -  | -  | + |
| Availability        | -  | ++ | +  | + |
| Autonomy          | -- | ++ | ++ | + |
| Traceability        | ++ | -  | +  | + |
| Performance         | ++ | +  | +  | + |
| Modifiability        | O  | ++ | +  | + |
| Maintainability      | -  | ++ | +  | + |
| Integrity           | ++ | -- | O  | + |
| Security            | -  | ++ | +  | + |
| Scalability         | -- | ++ | -  | + |
 
## Decision

Based on alternatives in the context of the business needs and a development team we think that modularize monolith is the best option for now. At the same time it opens the possibility to migrate to microservices when needed.

## Consequences

