# Dedicated health-check endpoint for services

Date: 2020-10-29

## Status

Accepted

## Context

The _ordering system_ is a dynamically developing system that starts as modularized monolith. Even in inital form it splited to a several services that have to be monitored. The system starts small, to save budget for cloud instances, but eventually grows towards many services. Based on technical and business metrics there should be a clear way to make a decision about extracting monolith's modules into services with smaller responsibility and ability to scale. 

There should be a clear metrics and vision about health statuses of services. It includes not only consumption of hardware resources, but also information about processing user's requests. 

## Decision

There is dedicated end-point that will provide information about health status of a service. 

For technical health checks we are using heartbeat pattern for fault detection. It alows us add services when necessary and supervisor will passively listening for incoming messages, instead of pushing requests (ping pattern). 

For business health checks there are sets of critical path scenarious. Each scenario started from dummy message from dedicated supervisor to measure execution of specific user scenario. Measurement includes correctness of execution and time.

## Consequences

Based on time and correctness of execution critical path scenarious we can proactively plan extraction of functionality and scaling cloud instances based on facts. 

Existense of dummy messages should be designed and implemented in the code that requires additional effort and increasing of cognitive complexity. We accept this trade-off as we get more facts about the real behaviour of system and can plan budget conciosly for next periods. 

Business health checks add additional level of safety in case of healthy technical case, but something in a business logic stucked. 

Technical checks partially can be supported by a platform of deployment. Technical checks helps admins to get immediate information about specific service in case of doubtful information from supervisor.  

## Risks 

Unaware of developers how to implement it correctly and possible impact on processing real requests from users. 
