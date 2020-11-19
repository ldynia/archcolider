# Stale data from fridges 

Date: 2020-11-19

## Status

Proposed 

## Context

Smart fridges system is an external system that provide vital information for the customer and for the *ordering system*. But, we do not control frequence of updates, data structure and management of available positions. Netherless, we have to provide service based on provided data and try to keep inventory on our side as precise as possible to avoid collision and situation when *user* can be unsatisfied by service. 

There is a risk that at some point in time we can't get actual data (offline, maintenance, throttling, caching, etc) how the *ordering system* should behave?

## Decision

We well cache and maintain data integrity about available stock in fridges on our side. Until we get new data from the *smart fridge system* and adjust our data.

## Consequences

Storing data about available stock add computational pressure to our system and cognitive complexity to model concurrency system for data integrity. We accept this consequences as we able to operates with estimated stocks and provide service for end users. This decision impact purchasing process and require business decision about the edge case when something was purchased but not delivered. 

There should be monitoring and alerting system for the *smart fridges* system. The team should be informed timely when data gap is more then defined gap.  

Ping pattern should be involved if *Smart Fridges* system do not have other health check handlers.  

**Risks:** 
- Loses on compensation by coupons for customer 

**Actions** 
- Define with business and tech team when to rise an alarm in case of data gap. It might be minutes or hours, for instance. 
