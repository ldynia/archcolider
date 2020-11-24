# Catalog caching on client side

Date: 2020-11-24

## Status

Proposed 

## Context

By the nature of the domain, meal catalog can't change every minute, it even won't change drastically every day. Most probably whole menu can be formed for a week and provided for the _ordering system_. Based on this assumtion we could upload the meal catalog once per day with amount of available SKU in fridges. Our estimations about the update package shows that the catalog with 20 meals could weight around 500kb-700kb without images. Even if it might be not significant amount of data for a single entry, multiplying it to number of users gives us big number for data transfering and data transfer is not free for us and users. 

The catalog updates with a meal amount might be organized as additional event message that will be very lightweight compare to entire catalog that will save us money on Cost of Ownership.  

## Decision

We going to upload and keep entire meal catalog on user's devices. 

## Consequences

Size of application will grow on user device as more kitchens provide their catalog but we ok with it. Also it increase code base and add logic on client side. From other side it will be easier to operate with local catalog. 

We should not upload on client device meal ids because it might be used for access code generation and we don't want to compromise the system. 

## Risk 

Catalog might be stale in terms of available meals, but we going to check possibility of purchase on backend anyway. 


