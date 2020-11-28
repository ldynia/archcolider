# Dedicated health-check endpoint for services

Date: 2020-10-29

## Status

Accepted

## Context

The _ordering system_ is a dynamically developing system that starts as a modularized monolith. Even in the initial form, it can be split up into several services that will have to be monitored. The system starts small, to save budget for cloud instances, but has the potential to grow towards many services. Based on technical and business metrics there should be a clear way to make a decision about extracting the monolith's modules into services with smaller responsibility scopes and improved scalability.

There should be a set of clear metrics and vision about health statuses of services. It includes not only consumption of hardware resources, but also information about processing user's requests.

## Decision

There is a dedicated end-point per service that will provide information about its health status.

For technical health checks we are using a heartbeat pattern for fault detection. It allows us to add services when necessary and the supervisor will passively listen for incoming messages, instead of pushing requests (ping pattern).

For business health checks there are sets of critical path scenarios. Each scenario starts with a dummy message from a dedicated supervisor to measure execution of specific user scenarios. Measurements will includes correctness of execution and time spent (duration).

## Consequences

Based on time spent and correctness of execution for critical path scenarios we can proactively plan extraction of functionality and scaling cloud instances based on facts.

Existence of dummy messages should be designed and implemented in the code this requires additional effort and increases cognitive complexity. We accept this trade-off as we get more facts about the real behaviour of the system and can plan budget conscious for next periods.

Business health checks add an additional level of safety in case of a healthy technical case, but something in a business logic stucked.

Technical checks partially can be supported by a platform of deployment. Technical checks help admins to get immediate information about specific a service in case of doubtful information from the supervisor.  

## Risks

Developers may be unaware of how to implement it correctly and the possible impact on processing real requests from users.

