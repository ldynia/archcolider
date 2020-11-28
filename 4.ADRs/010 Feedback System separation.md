# Feedback System separation

Date: 2020-10-29

## Status

Declined

## Context

A user would like to read or write a review for a meal that he has ordered. Businesses would like to obtain feedback on its service in order to improve it.

Two different feedback methods:
- surveys (occasional questionnaires about general aspects of the app/service)
- feedback (is an opinion about an order or app/service)

## Decision

We'll create a simple in app feedback system that will allow users to provide feedback about orders and service.
We'll incorporate surveys into feedback in order to take advantage of 3rd parties services which specialize in feedback acquisitions such survey monkey, google surveys, etc..


## Consequences

**Positive:** Reviews will encourage users to compose their own menus. Delegating surveys to 3rd parties services would allow food pharmacy to focus on improvement of core business. This decision will create loose coupling of the entities in the system.

**Negative**: Because, content can be vulgar, admin would have to moderate reviews.

**Neutral:** System will have to store images, therefore increasing costs of business operations.

## Reason

Incorporating 3rd party systems might cause security breaches of personal data. Cumbersome gathering, aggregating and store of results. Requires coordinated way of storing and processing results. Managing permissions to create, add, and stop surveys might be challenging.

