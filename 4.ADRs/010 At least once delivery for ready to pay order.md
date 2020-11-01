# At least once delivery for ready to pay order

Date: 2020-11-01

## Status

Proposed

## Context

Ready to pay orders should be handled with the special care. We'd like to guarantee "at least once delivery" for each order. This reqiure support of indempotent changes, or aware of the most recent state for oreder processing service.    

## Decision

Delivery of "ready to pay" orders performed by RabbitMQ with message acknolegement option. 

## Consequences

It will slightly decrease performance, but we get data integrity. Usage of EventStore and pojections with the order state will help to handle correct state changes for orders. 
