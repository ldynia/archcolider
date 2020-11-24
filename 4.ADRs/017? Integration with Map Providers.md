# Integration with Map Providers.

Date: 2020-11-24

## Status

Proposed 

## Context

Application should be integrated with 3rd party geolocation providers to help the user reach the location of the Smart Fridge. Currently, we consider three maps providers Google Maps, OpenStreetMap and Here.com. Google Maps integrates well with mobile and web platforms and provides a rich API as well as well known user interface to operate with. Here.com are the maps created formally by Nokia. Hear.com service is free for up to 250K transactions per month. On the other hand OpenStreetMap are open source and free of charge.

## Decision

Based on the business model (as there will be more subscribed users, who knows the location precisely ) we have decided to integrate with OpenStreetMap API as its open-source -there will be no added expenditures for the business.

## Consequences

As OpenStreet map is a open-source there may be chance of limited or no support in future.
Due to the nature of the project, excessive exchange of data through the API is not welcome, and users may get blocked without notice when making too many data requests.

## Governance

While maintaning the application, there is a need of constant surveillance on the support of maps.
