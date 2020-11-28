# Every meal delivery has pick up pin code

Date: 2020-10-28

## Status

Accepted

## Context

Network connection might be lost, when a meal is delivered to a fridge and a user comes to grab it. Then the fridge can't check data of the user online by card swapping, or in-app distance opening.
But the fridge has a pin pad keyboard and still has quite sophisticated software and internal memory to process orders.

Update 2020-11-24:

We expect that every meal has its own unique id provided by the kitchen because some meals might be customized from the general catalog. Let's say lactose-free lasagna should be addressed to a specific user.

Then, at the purchase or production process, we can update the user's device with the meal's unique id and generate an access code based on meal ID.

## Decision

Meals dispatched from a Ghost Kitchen, will have a special 6-8 digit code.

## Consequences

Now the user can grab the meal even if the smart-fridge is disconnected from the network at the moment of picking up the meal.

Pin codes for meals should be formed upfront and delivered early to devices (smart-fridge and user-device). Possibly, there might be a mechanism to update those codes with prepared meal delivery. The pin code should be quite long to lower the chance of a brute-force attack.   

**Bonus feature:** it's easier to delegate meal grabbing to other people.

**Risks:** Someone can be so lucky that they can guess a pin code from a first attempt.

**Arguments:** 8th long digit codes are too long to type!
