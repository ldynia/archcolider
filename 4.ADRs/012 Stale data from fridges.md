# Stale data from fridges

Date: 2020-11-19

## Status

Proposed

## Context

Smart fridges system is an external system that provide vital information for the customer and for the *ordering system*. But, we do not control frequency of updates, data structure and management of available positions. Nonetheless, we have to provide service based on provided data and try to keep inventory on our side as precise as possible to avoid collision and situation when *user* can be unsatisfied by service.

There is a risk that at some point in time we can't get actual data (offline, maintenance, throttling, caching, etc) how the *ordering system* should I behave?

The occasional user (who pays cash) is a major factor in this issue. Any pre-paid meals that can still be picked up in an offline scenario don't really contribute to the stale data issue as the payment server must already have done its job.

## Decision

We well cache and maintain data integrity about available stock in fridges on our side. Until we get new data from the *smart fridge system* and adjust our data.

## Consequences

Storing data about available stock adds computational pressure to our system and cognitive complexity to model concurrency system for data integrity. We accept these consequences as we are able to operate with estimated stocks and provide service for end users. This decision impacts the purchasing process and requires a business decision about the edge case when something was purchased but not delivered.

There should be monitoring and alerting system for the *smart fridges* system. The team should be informed timely when a data gap is more than a defined gap.  

Ping pattern should be involved if *Smart Fridges* system do not have other health check handlers.  

**Risks:**
- Loses on compensation by coupons for customer

**Actions**
- Define with the business and tech team when to raise an alarm in case of a data gap. It might be minutes or hours, for instance.
