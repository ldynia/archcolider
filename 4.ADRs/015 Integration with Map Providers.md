# Integration with Map Providers.

Date: 2020-11-24

## Status

Proposed

## Context

Application should be integrated with 3rd party geolocation providers to help the user reach the location of the Smart Fridge. Currently, we consider below map providers to integrate with our application.


| Provider           | Pricing Criteria                                                          | Pros                 | Links                                         |
| :------------------|:-------------------------------------------------------------------------:| --------------------:| ---------------------------------------------:|
| OpenStreet Maps    | Free                                                                      | No-cost, Open-source | [Documentation](https://wiki.openstreetmap.org/wiki/Main_Page)|
| TomTom             | Free for 2,500 requests daily,$0.42–$0.50 for each subsequent 1000        | Better Navigation    | [Documentation](https://developer.tomtom.com/)               |
| MapBox             | Free for 50,000 requests daily, $0.50 for each subsequent 1,000           | custom map features | [Documentation](https://docs.mapbox.com/)     |
| Here Maps          | Free for 250,000 requests monthly, $1 for each subsequent 1,000 OR $449 for 1,000,000 requests monthly           | Better visualization  services | [Documentation](https://developer.here.com/pricing)     |



## Decision

Based on the business model and the volume of data now and in near future , as there will be more subscribed users, who knows the location precisely . We have decided to integrate with Here maps as it has good market reach and first 25K requests were free.

## Consequences

As of now 250K transactions per month looks decent for the business model , when the business grows, it should be ready to upgrade to premium solution

## Governance

While maintaining the application, there is a need of constant surveillance on the number of requests per month to avoid additional expenditure.
