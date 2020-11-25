# Cache the meal catalogue on client side.

Date: 2020-11-19

## Status

Proposed 

## Context

User satisfaction and speed of applicaton is our priority and in case of slow\unstable connection we'd like to provide as less delay as possible in catalog browsing. Users should not experience long load screens and delays during browsing. We can safely assume that menu catalog won't have drastic changes during a day and we can cache catalog with estimated number of meals in each fridge in user's area. So we can upload this information upfront. 

Purchase process, i.e. payment confirmation always take some time and users get used to it and this can be used to attempt actualize certain position in menu. 

By the nature of the domain, meal catalog can't change every minute, it even won't change drastically every day. Most probably whole menu can be formed for a week and provided for the ordering system. Based on this assumtion we could upload the meal catalog once per day with amount of available SKU in fridges. Our estimations about the update package shows that the catalog with 20 meals could weight around 500kb-700kb without images. Even if it might be not significant amount of data for a single entry, multiplying it to number of users gives us big number for data transfering and data transfer is not free for us and users.

The catalog updates with a meal amount might be organized as additional event message that will be very lightweight compare to entire catalog that will save us money on Cost of Ownership.

## Decision

We will cache menu catalog and do actual check during purchase confirmation. Before that moment no connection required. 
We going to upload and keep entire meal catalog on user's devices.

## Consequences

Users can experience longer dealy during purchase confirmation step, but it's ok from our perspective. 

The app and PoS would have more logic related to storing data and scheduled data updates, but those processes are simple in their nature and do not require excessive design. 

Meal catalog might require additional fine graned API to support checking available stocks for a particular meal in user's area. Geo location services involved anyway so it won't affect overall flow. 

Size of application will grow on user device as more kitchens provide their catalog but we ok with it. Also it increase code base and add logic on client side. From other side it will be easier to operate with local catalog.

We should not upload on client device meal ids because it might be used for access code generation and we don't want to compromise the system.

## Risks
Catalog might be stale in terms of available meals, but we going to check possibility of purchase on backend anyway.
