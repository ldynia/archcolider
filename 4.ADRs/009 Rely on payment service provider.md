# Rely on payment service provider

Date: 2020-10-31

## Status

Proposed

## Context

The _ordering system_ should accept a wide variety of payment methods to satisfy user's expectations and increase user base. The number of payment system is significant and each of them have nuances in API and ways of communication.  

## Decision

Use a 3rd party payment provider to delegate dealing with different payment systems.

## Consequences

We save time required for implementing large payment systems but have to track trends and pay fees for processing money transactions.

Internal payment system still should leave room for implementing additional adapters for emerging payment systems.

Risks: Need to be careful while processing the personal/demographic details from user, w.r.t compliance and auditing.
