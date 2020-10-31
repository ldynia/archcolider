# 1. Event sourcing usage

Date: 2020-10-30

## Status

Proposed 

## Context

Food Farmacy works with external individual users and depends on reputation. In such environment the time and accuracy of resoling users complains is essential. Thus, there should be a way to store all intermediate changes that used did. Keeping only final state of a domain entities won't help to understand how did we end up with a specific state. 

The _ordering system_ going to evolve as company grows and not all aspects clear at the beginning. There should be an option for gracefull migration from one data model and data completenes to another. 

User engagement is one of the business goals and there should be data for analysis of user's actions and behaviors to build a better model of new users engagement.  

## Alternatives 

**Snapshot usage** 

A widely-known approach that in use for years. There are might be separated systems that logs users' actions and the most recent state of the correspondent entities. Usuallu. users' action not even recorded, and only the final state presented as a source of truth. In case of programatical error for a such approach it's possible to get incorrect state of the entity, or impossible reconstruct the way how an entity ended up in a presented state. Application logs won't help much or will be too combersome to investigate a particular case. 

From other side such approach is easy to emplement and usually do not require any special knowledge. 

In case of recording all events and managing snapshot it requires manual management and correlating of those actions. We forseen unnecessary complexity in this case and a higher probability of making mistake from programming standpoint. Correlated transactional update will have significant impact on performance. 

**Event sourcing**  

Quite a new approach for many developers. In fact some benefits and drawbacks were described for a snapshot usage. Without support of a dedicated tool for eventsourcing a correct and convinient implementation will require time and followin support from the development team. If there will be a tool for handling eventstreams, building snapshots and sending notification for other parts of the system that something changes it would be very handy. Thankfuly such tool exists, it's the EventSource - OSS system for event sourcing. 

There is some risks in adopting such tool, but benefits are much more promising in terms of having immutable history of changes, automatic projections (snapshots) and notifying suscribers for a specific events. 

## Decision

Event sourcing approach gives us full history of changes and can help investigate issues and user's complaints. With support of EventSource storage the main issue with sychronizing updates and read models seems manageable.

## Consequences

New system might be used in suboptimal way until developers grasp the idea behind and adopt working pattern to a new paradigm. 

Preferable start with SaaS solution to remove support and scale issues. 
