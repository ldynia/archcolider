# User's scenarios (journeys)

This section shows a generic example of a user journeys. After reading this section reader should know who are the stakeholder within the system, how the user interacts with the system and what are the results of an interaction.

## 1 Scenario: Purchase of a meal by a subscriber

Bellow diagram illustrates a purchase order within the system. User journey starts at the moment of browsing a meal from the catalog and ends when a meal is picked up by the user. Dotted lines represent optional interactions in the system.

![Subscriber Journey](../img/user%20journey/Subscriber.png)

### Stakeholders
* Subscriber - Interested in choosing a meal, picking it up and eventually rating it and writing a review.
* Cashier - Is a Point of Sale operator, facilitates  meal purchase for unsubscribed users.

### Risks
Access code generation can be cumbersome to implement. We might introduce **PIN** instead.
We need to put in place mechanisms that handles submissions of two valid coupons.
Handling of cash payment. This should be discussed further.

## 2 Scenario: Purchase of a meal by a subscriber

This journey illustrates a purchase of a meal by an occasional user - a user who is not registered in the system. The idea of occasional user is to convert him into a subscriber

![Occasional User Journey](../img/user%20journey/Ocasional%20User.png)

### Stakeholders

* Occasional User - Interest of purchasing a meal without being registered in the system.
* Cashier - Is a Point of Sale operator, facilitates  meal purchase for unsubscribed users.

### Risks
We need to put in place mechanisms that handles submissions of two valid coupons.
Providing access code to the smart fridge for meal pick up.

## 3 Scenario:

Bellow user story, show a use case where some unexpected error (perhaps mechanical) prevents the user from picking up the meal. Outcome of the events is creation of complaint by a user receiving new meal (or compensation) later on.

![Subscriber Error Journey](../img/user%20journey/Error%20-%20Subscriber.png)


### Stakeholders

* Subscriber - Interested in choosing a meal, picking it up and eventually rating it and writing a review.
* Admin - Backend user who moderates content and resolves subscribes complains.

### Risks
There might be a risk that a subscriber will be cached in a loop on submitting a valid code in a system that cannot validate the access code. However, this case should be mitigated by storing access codes locally.
