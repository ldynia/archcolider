# User's scenarious (journeys)

This section shows a generic example of a user journeys. After reading this section reader should know who are the stakeholder within the system, how the user interacts with the system and what are the results of an interaction.

## Scenarion 1: Purchase of a meal by a subscriber

Bellow diagram illustrates a purchase order within the system. User journey starts at the moment of browsing a meal from the catalog and ends when a meal is picked up by the user. Dotted lines represent optional interactions in the system.

![Subscriber Journey](https://github.com/ldynia/archcolider/blob/master/img/user%20journey/Subscriber.png)

### Stakeholders 
* User
* Cashier -located at the Point of Sale

### Risks
Access code generation can be cumbersome to implement. We might introduce **PIN** instead. 
We need to put in place mechanisms that handles submissions of two valid coupons.
Handling of cash payment. This should be discussed further.

## Scenarion 2: Purchase of a meal by a subscriber

This journey illustrates a purchase of a meal by ocasionall user - a user who is not registered in the system. The idea of ocasionall user is to convert him into a subscriber

![Ocasional User Journey](https://github.com/ldynia/archcolider/blob/master/img/user%20journey/Ocasional%20User.png) 

### Stakeholders 

* Ocasional User
* Cashier -located at the Point of Sale

### Risks
We need to put in place mechanisms that handles submissions of two valid coupons.
Providing access code to the smart fridge for meal pick up.

## Scenario 3: 

Bellow user story, show a use case where some unexpected error (perhaps mechanical) prevents the user from picking up the meal. Outcome of the events is creation of complaint by a user receiving new meal (or compensation) later on.

![Subscriber Error Journey](https://github.com/ldynia/archcolider/blob/master/img/user%20journey/Error%20-%20Subscriber.png)


### Stakeholders 

* Subscriber
* User with Admin privilage

### Risks
