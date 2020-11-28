# Stale data from fridges

Date: 2020-11-19

## Status

Proposed

## Context

The smart fridge system is an external system that provides vital information for the customer and the *ordering system*. But, we do not control the frequency of updates, data structure, and management of available positions. Nonetheless, we have to provide our service based on the provided data and try to keep inventory on our side as precise as possible to avoid collision and situations where the user might be dissatisfied with our service.

There is a risk that at some point in time we can't get actual data (offline, maintenance, throttling, caching, etc). How will the ordering system handle such situations?

The occasional user (who pays cash) is a major factor in this issue. Any pre-paid meals that can still be picked up in an offline scenario don't really contribute to the stale data issue as the payment server must already have done its job.

## Decision

We will cache and maintain data integrity about the available stock in fridges on our side. Until we get new data from the *smart fridge system* at which point the data will be adjusted.

## Consequences

Storing data about the available stock adds computational pressure to our system and cognitive complexity to the concurrency model of the system for data integrity. We accept these consequences as we are able to operate with the estimated stocks and provide our service for end-users. This decision impacts the purchasing process and requires a business decision about the edge case when something was purchased but not delivered.

There should be a monitoring and alerting system for the *smart fridges* system. The team should be informed timely when a data gap is more than the defined gap.  

A ping pattern should be involved if *Smart Fridges* systems do not have other health check handlers.  

**Risks:**
- Loses on compensation by coupons for customer

**Actions**
- Define with the business and tech team when to raise an alarm in case of a data gap. It might be minutes or hours, for instance.
