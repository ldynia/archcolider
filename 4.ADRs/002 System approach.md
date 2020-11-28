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

| | Monolith | Microservices | Micro-kernel |
|----|----|----|-----|
| Ease of Deployment  | ++ | -  | -  |
| Availability        | -  | ++ | +  |
| Autonomy          | -- | ++ | ++ |
| Traceability        | ++ | -  | +  |
| Performance         | ++ | +  | +  |
| Modifiability        | O  | ++ | +  |
| Maintainability      | -  | ++ | +  |
| Integrity           | ++ | -- | O  |
| Security            | -  | ++ | +  |
| Scalability         | -- | ++ | -  |
 
## Decision

Based on alternatives in the context of the business needs and a development team we think that micro-kernel approach is the best option for now. At the same time it opens the possibility to migrate to microservices when needed.

Can be converted to highly modularized monolith with characteristics of micro-kernel approach

## Consequences

The major parts of the system will require careful API management to make possible unified access to the kernel. At the same time it gives a solid base for the development and tracking what should be converted to microservices.

Micro-kernels require more attention from developers, but still allow independent development of major parts and extend main functionality with 3rd party plug-ins.
