Date: 2020-10-29 

Busines Driver nr: 6.001 - 
User get notification about any significant action that related to actual ordering: 
payment process (initializing and result), 
availability of food for pickup, 
canceling, out of stock situation.

## Status

Proposed (Lukasz)

## Context

User shoul be able to track the propagation of events for orders that he created.

## Decision

We'll provide notifications service that will provide, sms, email, push, in-app messages.
We'll provide notifications about payment process (initializing and result)
We'll provide notifications about availability of food for pickup
We'll provide notifications about canceling, out of stock situation
We'll provide allow admin to crate custom notification messages.
We'll provide user options for disabling notifications.


## Consequences

**Positive:** Createing HA solution for Order availability, Introudcing *messaging* as major protocol for information propagation.  

**Negative:**
