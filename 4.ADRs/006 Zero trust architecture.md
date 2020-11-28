# Zero trust architecture

Date: 2020-10-30

## Status

Proposed

## Context

The _ordering system_ communicates with upstream and downstream systems in a cloud environment and we can't rely on an assumption that requests from the same subnetwork are safe.

The _ordering system_ is implemented as a modularized monolith and those modules will eventually be extracted to become dedicated services. We have to secure such calls at an early stage to make it easier to migrate from module to service.

## Decision

Internal calls from modules should contain security info with auth and claims info from the very beginning.

## Consequences

Applying such an approach will add complexity to communication between modules within the same domain. This may not be obvious to many developers. In turn, it allows for proper separation of communication between modules and readiness for extracting modules as services.

The suggested approach will require involving identity service and increase the complexity of internal logic within monolithic services, but simplify further scaling with dedicated services.

Some optimization within monolithic modules will be required when modules are incorporated.

## Reference

[Zero Trust Architecture](https://www.thoughtworks.com/radar/techniques?blipid=202005092)
