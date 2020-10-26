# Functional Requirements 

The business goal (reminder): 

_A “ghost kitchen” (food preparation and cooking facility set up for the preparation of delivery-only meals.) needs *an ordering system* to allow users to have visibility of what items are available, purchase, and pick up items at any one of their points of sale / smart-fridge._

## Requirements provided by owner

1. Must integrate with 3rd party smart fridges to obtain inventory and purchase activity
2. Smart Fridges Produce item inventory levels and purchases. The smart fridges have a cloud based management system that handles communication with the Smart Fridge so obtaining this data would be through an API.
3. Must integrate with point of sale system at kiosks
4. The Kiosk is a sublet space inside another business where we will sell our product but have an employee handle the transactions through a point of sale. The same data should be accessible through the POS systems API’s.
5. Mobile and Web accessible
6. Support providing feedback on items of verified purchases and in app surveys.
7. Accept coupons and promotional pricing
8. Send inventory updates to central kitchen

### Clarification and possible out of scope items 

Req #1 sounds quite vauge and out of scope as there independent system (we'll call it Kiosk Mgmt System) that provide communictation and managing of smart-fridges (see Req #2). From out perspective it sounds like the responsiblity of such integration and communication lays out of responsibility of the Ordering system. **Need clarification.**

Req #3 tells that the Ordering system should integrate with point of sales. So from our perspective it is sort of confirmation from the seller. Here using cash for non-subscribers might be a valid _use case_. 

Req #4 groups with Req #3 and provide additional information about the environment and context. If we transform it to the _use cases_, then it will be: 
- System should support and engage ocassional users. 
- System should support cash payments

Req #5 is clear and telling about user communication channels and egagement. Then, possible _use cases_:
- System should support and engage subscribers and known users

Req #6 fully is about user engagement in various aspects that might be not defined yet. Then, possible _use cases_:
- System should be extensible for new form of engagements including, but not limited by surveys, direct feedbacks, reviews, discount\coupon programs and so on. 

Req #7 is extension of Req #6

Req #8 is about integration. 

_Assumptions_: 
1. Central kitchen already uses some tracking system that have a some form of API that accepts writes. 
2. _Inventory updates_ are not limited by changes in stock of smart-fridges for refill.
3. _Inventory updates_ can be formed by user's request of desired meal. User can be subscriber or known user. 
4. _Inventory updates_ formed by scheduling system from subscibers menu for a week/month. 

_Questions_:
1. How often central kitchen should get updates? Why it's important - kitchen by itself do not working 24/7. Kitchen should have refilment of supply
2. How to provide feedback to orderer if order can't be fullfiled in desired time frame? Are there timeframes of delivery in general? 

## Functional areas

Based on business goal provided by the owner we can exctact following functional areas: 

**Core context** 

1. Reservation of food - 
1. Picking up food
1. Point Of Sales integration with Ordering system
1. Food catalog (visibility of items)

**Support context** 

1. Ordering system
1. Purchasing system

**Generic context**

1. Integration between internal systems
1. User applications
1. Notification system 
