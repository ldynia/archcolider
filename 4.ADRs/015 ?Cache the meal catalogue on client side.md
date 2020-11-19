# Cache the meal catalogue on client side.

Date: 2020-11-19

## Status

Proposed 

## Context

User satisfaction and speed of applicaton is our priority and in case of slow\unstable connection we'd like to provide as less delay as possible in catalog browsing. Users should not experience long load screens and delays during browsing. We can safely assume that menu catalog won't have drastic changes during a day and we can cache catalog with estimated number of meals in each fridge in user's area. So we can upload this information upfront. 

Purchase process, i.e. payment confirmation always take some time and users get used to it and this can be used to attempt actualize certain position in menu. 

## Decision

We will cache menu catalog and do actual check during purchase confirmation. Before that moment no connection required. 

## Consequences

Users can experience longer dealy during purchase confirmation step, but it's ok from our perspective. 

The app and PoS would have more logic related to storing data and scheduled data updates, but those processes are simple in their nature and do not require excessive design. 

Meal catalog might require additional fine graned API to support checking available stocks for a particular meal in user's area. Geo location services involved anyway so it won't affect overall flow. 
