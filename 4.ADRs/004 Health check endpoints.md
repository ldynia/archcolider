# Dedicated health-check endpoint for services

Date: 2020-10-29

## Status

Accepted

## Context

The _ordering system_ is a dynamically developing system that starts as modularized monolith. Even in initial form it splitted to a several services that have to be monitored. The system starts small, to save budget for cloud instances, but eventually grows towards many services. Based on technical and business metrics there should be a clear way to make a decision about extracting monolith's modules into services with smaller responsibility and ability to scale.

There should be a clear metrics and vision about health statuses of services. It includes not only consumption of hardware resources, but also information about processing user's requests.

## Decision

There is a dedicated end-point that will provide information about the health status of a service.

For technical health checks we are using heartbeat pattern for fault detection. It allows us to add services when necessary and the supervisor will passively listen for incoming messages, instead of pushing requests (ping pattern).

For business health checks there are sets of critical path scenarios. Each scenario started with a dummy message from a dedicated supervisor to measure execution of specific user scenarios. Measurement includes correctness of execution and time.

## Consequences

Based on time and correctness of execution critical path scenarios we can proactively plan extraction of functionality and scaling cloud instances based on facts.

Existence of dummy messages should be designed and implemented in the code that requires additional effort and increasing cognitive complexity. We accept this trade-off as we get more facts about the real behaviour of the system and can plan budget conscious for next periods.

Business health checks add an additional level of safety in case of a healthy technical case, but something in a business logic stucked.

Technical checks partially can be supported by a platform of deployment. Technical checks help admins to get immediate information about specific service in case of doubtful information from the supervisor.  

## Risks

Unaware of developers how to implement it correctly and possible impact on processing real requests from users.

