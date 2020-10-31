# Service readiness checks

Date: 2020-10-30

## Status

Proposed

## Context

Currently there are only several services planned, but most of them requires time for initialization (warming cache for instance) and they can't start processing requests from other services immediatly. The situation might arise at restarting of service, introducing a new instance, or some other situations. 

If service is not ready for processing a request the timeout might happen and supervisor might decide that there should to spin up a new instance that lead to cascade effect and higher bills in the end. 

## Decision

Health check endpoint provide information about rediness of processing requests and other services should respect this information. 

## Consequences

By this implementation we avoid [dog pile](https://www.sobstel.org/blog/preventing-dogpile-effect/) effect for services that usually can handle all request with a single instance, but becasue of accomulated requests time for processing significantly increases that produce false positive alarms for admins and supervisor system. 

