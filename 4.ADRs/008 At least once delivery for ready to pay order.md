# At least once delivery for "ready to pay" order

Date: 2020-11-01

## Status

Proposed

## Context

"Ready to pay" orders should be handled with special care. We'd like to guarantee "at least once delivery" for each order. Order payment processing is a business-critical scenario because selling meals is the whole point. In this case, there should be a guarantee, that the order store and payment processor can pick the order for execution.

At the same time, it's very important to avoid double payments, because of concurrency issues. When an order with a "Ready to pay" state arrives, in theory, it can be processed one or more times, but it should not lead to doubled, tripled, and so on charges from a user's account.

## Decision

Delivery of "ready to pay" orders performed by a MessageQueue software with a message acknowledgment option. Additionally, we expect that the order comes with a unique id from client devices at the time of processing. During order processing, the existence of the order with the same id can be checked and the version number should be used for staleness validation. In this case, the event with the same version will be discarded by the processing service.    

## Consequences

It will slightly decrease performance, but we get data integrity. Usage of EventStore and projections with the order state will help to handle correct state changes for orders.
