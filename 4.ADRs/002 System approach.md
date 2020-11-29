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
| Ease of Deployment  | ++ | -  | -  | ++ |
| Availability        | -  | ++ | +  | - |
| Autonomy          | -- | ++ | ++ | + |
| Traceability        | ++ | -  | +  | O |
| Performance         | ++ | +  | +  | ++ |
| Modifiability        | O  | ++ | +  | + |
| Maintainability      | -  | ++ | +  | + |
| Integrity           | ++ | -- | O  | + |
| Security            | -  | ++ | +  | ++ |
| Scalability         | -- | ++ | -  | + |

## Decision

Based on alternatives in the context of the business needs and a development team we think that modularized monolith is the best option for now. At the same time it opens the possibility to migrate to microservices when needed.

## Consequences

The main benefits come in the development and deployment area. The team could save a lot or resources setting up dev/test/qa/prod environments. The cost of development and cognitive complexity is low level because working on the same code base requires less synchronization meetings.

Extensibility and modifiability with the proposed approach should be on a high level with properly designed facades between modules.

Extra care and discipline should be applied for inter module communication, or it will be just a monolith with a tendency towards "the big ball of mud". Every module should keep subdomain concepts clean and sometimes copy-pasting a part of code is the best approach to avoid hidden dependencies.
