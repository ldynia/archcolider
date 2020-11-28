# Zero trust architecture

Date: 2020-10-30

## Status

Proposed

## Context

The _ordering system_ communicates with upstream and downstream systems in a cloud environment and we can't rely on an assumption that requests from the same subnetwork are safe.

Also, the _ordering system_ implements as modularized monolith and those module will be eventually extracted to become a dedicated services. We have to secure such calls at an early stage to make it easier to migrate from module to service.

## Decision

Internal calls from modules should contain security info with auth and claims info from the very beginning.

## Consequences

Applying such an approach will add complexity to communication within one domain between modules and not obvious for many developers. In turn it allows for proper separation of communication between modules and readiness for extracting modules as services.

Suggested approach will require involving identity service and increase complexity of internal logic within still monolithic services, but simplify further scaling with dedicated services.

Some optimization within monolithic modules will be required while modules incorporated.

## Reference

[Zero Trust Architecture](https://www.thoughtworks.com/radar/techniques?blipid=202005092)
