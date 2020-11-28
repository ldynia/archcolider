# Cache the meal catalogue.

Date: 2020-11-19

## Status

Proposed

## Context

User satisfaction and speed of the application is our priority and in case of a slow\unstable connection, we'd like to have the smallest delay possible in catalog browsing. Users expect quick response times. We can safely assume that the menu catalog won't have drastic changes during a day and we can cache the catalog with an estimated number of meals in each fridge in the user's area. Most probably the whole menu can be formed for a week and provided for the ordering system. Based on this assumption we could upload the meal catalog once per day with the amount of available Stock Keeping Unit (SKU) in fridges. Our estimations on the update package sizes show that a catalog with 20 meals could weigh around 500kb-700kb without images. Even if it might not be a significant amount of data for a single entry, multiplying it by the number of users gives us a large amount of data to transfer which isn't free for us and the users. The catalog updates with a meal amount might be organized as additional event messages that will be very lightweight compare to the entire catalog that will save us money on the Cost of Ownership. So we can upload this information upfront.

The purchase process, i.e. payment confirmation, always takes some time and users get used to it and this can be used to attempt to actualize a certain position in the menu.

## Decision

We will cache the menu catalog and do an actual check during purchase confirmation. Before that moment no connection will be required.
We are going to upload and keep the entire meal catalog on the users' devices.

## Consequences

Users can experience longer delays during the purchase confirmation step, but it's ok from our perspective.

The app and PoS would have more logic related to storing data and scheduled data updates, but those processes are simple in their nature and do not require excessive design.

Meal catalog might require additional fine-grained API to support checking the available stocks for a particular meal in the user's area. Geo-location services involved anyway so it won't affect the overall flow. The size of the application will grow on the users' devices as more kitchens provide their catalog but we are ok with it. Also, it increases the code base and adds logic on the client-side. On the other side, it will be easier to operate with a local catalog.

We should not upload on client device meal ids because it might be used for access code generation and we don't want to compromise the system.

## Risks

Catalog might be stale in terms of available meals, but we are going to check the possibility of purchase on the backend anyway.
