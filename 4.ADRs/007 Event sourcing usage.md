# 1. Event sourcing usage

Date: 2020-10-30

## Status

Proposed

## Context

Food Farmacy works with external individual users and depends on reputation. In such an environment the time and accuracy of resolving users' complaints are essential. Thus, there should be a way to store all intermediate changes that are used. Keeping only the final state of a domain entity won't help to understand how we end up with a specific state.

The ordering system going to evolve as the company grows and not all aspects clear at the beginning. There should be an option for graceful migration from one data model and data completeness to another.

User engagement is one of the business goals and there should be data for analysis of a user's actions and behaviors to build a better model for new user engagements.

## Alternatives

**Snapshot usage**

A widely-known approach that has been in use for years. There might be separate systems that log users' actions and the most recent state of the correspondent entities. Usually. users' actions not even recorded, and only the final state presented as a source of truth. In case of programmatic errors of such an approach, it's possible to get the incorrect state of the entity, or impossible reconstruct the way how an entity ended up in a presented state. Application logs won't help much or will be too cumbersome to investigate a particular case.

On the other side, such an approach is easy to implement and usually doesn’t require any special knowledge.

In the case of recording all events and managing snapshots, it requires manual management and correlating of those actions. We foresee unnecessary complexity in this case and a higher probability of making mistakes from a programming standpoint. Correlated transactional updates will have a significant impact on performance.

**Event sourcing**  

Quite a new approach for many developers. In fact, some benefits and drawbacks were described for snapshot usage. Without the support of a dedicated tool for event sourcing, a correct and convenient implementation will require time and continued support from the development team. If there will be a tool for handling event streams, building snapshots, and sending notifications for other parts of the system that something changes it would be very handy. Thankfully such a tool exists, it's the EventSource - OSS system for event sourcing.

There are some risks in adopting such a tool, but the benefits are much more promising in terms of having an immutable history of changes, automatic projections (snapshots), and notifying subscribers of specific events.

## Decision

The event sourcing approach gives us a full history of changes and can help investigate issues and users' complaints. With the support of EventSource storage, the main issue with synchronizing updates and read models is manageable.

## Consequences

A new system might be used in a suboptimal way until developers grasp the idea behind event sourcing and adopt working patterns to this new paradigm.

Preferable start with SaaS solution to remove support and scale issues.
