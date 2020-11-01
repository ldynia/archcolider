# Feedback System separation

Date: 2020-10-29 

## Status

Declined

## Context

A user would like to read or write a review for a meal that he has ordered. Business would like to obtaing feedbacks on its service in order to imporove it.

Two diffrent feedback methods:
- surveys (ocasional questionaries about general aspects of the app/service)
- feedback (is an opinion about an order or app/service)

## Decision

We'll create a simple in app feedback system that will allow users to provide feedback about orders and service.
We'll incorporate survey into feedback in order to take adventages of 3rd parties services which specilize in feedback aquisitions such survey monkey, google surveys, etc..


## Consequences

**Positive:** Reviews will encurage users to compose own menus. Delegating surveys to 3rd parties services would allow food pharmacy to focus on improvment of core business. This decision will create lose coupling of the entities in the system.

**Negative**: Because, content can be voulgar, admin would have to moderate reviews.

**Neutral:** System will have to store images, therfore increasing costs of businesss operations.
