# Zero trust architecture

Date: 2020-10-30

## Status

Proposed 

## Context

The _ordering system_ communiate with upstream and downstream systems in a cloud environment and we can't rely on an assumption that requests from the same subnetwork is safe. 

Also, the _ordering system_ implements as modularized monolith and those module will be eventually extracted to become a dedicated services. We have to secure such calls on a early stages to make it easer migrate from module to service.

## Decision

Internal calls from modules should contain security info with auth and claims info from the very beginning. 

## Consequences

Applying such approach will add complexity to communication within one domain between modules and not obvious for many developers. In turn it allows to control proper separation of communication between modules and readiness for extracting modules as services. 

Suggested approach will require involving idenitiy service and increase complexity of internal logic withing still monolithic services, but simplify further scaling with dedicated services. 

Some optimization within monolitic modules will be required while modules incorporated. 
