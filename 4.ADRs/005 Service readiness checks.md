# Service readiness checks

Date: 2020-10-30

## Status

Proposed

## Context

Currently there are only several services planned, but most of them require time for initialization (warming cache for instance) and they can't start processing requests from other services immediately. The situation might arise when restarting a service, introducing a new instance, or some other situations.

If a service is not ready for processing a request, the timeout might happen and the supervisor might decide that there should be a new instance that leads to a cascading effect and higher bills in the end.

## Decision

Health check endpoints provide information about readiness of processing requests and other services should respect this information.

## Consequences

Through this implementation, we avoid [dog pile](https://www.sobstel.org/blog/preventing-dogpile-effect/) effect for services that usually can handle all requests with a single instance, but because of accumulated requests time for processing significantly increases that produce false-positive alarms for admins and supervisor system.
