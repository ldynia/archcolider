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

1. Meal reservation (Req #8, #5, #6)
1. Picking up meal (Req #3, #4)
1. Point Of Sales integration with Ordering system (#3, #4)
1. Meal catalog (visibility of items) (#7, #6)
1. Ordering system - internal subsystem
1. Scheduling meals

**Support context** 

1. Purchasing system

**Generic context**

1. Integration between internal systems
1. User applications
1. Notification system 

### Meal reservation 

Make available upfront reservation of meals based on time. In general it might be instatly available meals in the fridge and on-demand from catalog. 

Sunny day scenarios: 
1. User (Subscriber, Known user) browse the meal catalog, select avalable meals in fridges, book it and pay at pickup time of a meal.   
2. Subscriber forming a manu schedule and get notification when a meal is available each day. Menu is prepaid.  

Extended use cases: 
1. 

Questions: 
1. Is there option for prepaiment to book a meal
2. For how long upfront user can reserve a meal? 
3. Is Subscriber didn't pick up a meal during a time frame can it be listed in common catalog? 

Risks: 
1. User booked a meal, but not picked up. Option: prepay to acomplish operation. 


### Picking up meal 

Responsible for "direct" communication with a fridge and the ways who picking up process might be executed. 

Sunny day scenarios: 
1. Subscriber use stored in the app banking card to authorize and pick up a meal. Kiosk knows the order associated with the user upfront. 
2. Known user selecting a meal from catalog, use card for payement and picking up a meal. 
3. Ocassional user with help of PoS Seller order a meal. 
4. Meal arrived to a fridge and user get notification of availability. 

Extended use cases: 

Risks: 
1. Loss of connection. Options: 1) Generating one time recovery codes. 2) Swiping the card and getting a meal. 
2. Meal is stuck in the fridge. Options: 1) User take a photo and file a complaint.

### Point Of Sales integration

Specail app (or part of frontend) with user impersonation by PoS admin. Allows reuse the same logic as for other users.  

Sunny day scenarios: 
1. Occassional user make an order, PoS admin perform order in the PoS app. Type of payment doesn't matter. 
2. Subscriber coming to grab a meal, provide a code/message that appears in PoS app, based on this info PoS Admin provide a meal. 

Extended use cases: 

Risks: 
1. Loss of connection. Options: 1) Eventual consistency of operations. Send data when network will be available. 2) Recovery codes from Subscriber


### Meal catalog

Responsible for providing information about available meals in fridges and on-demand meals. 

Sunny day scenarios: 
1. Actual meals for each fridge is available for browsing. Each item contains description, price, exact place.  

Extended use cases: 
1. User can set desired area of fridges and get items based and this area 
2. User can set filters based on alergens and content 

Risks:
1. Can the catalog contain meals out of order, but with general availability for ordering withing some time frame? 
2. How often data should be updated? 

### Ordering system

Keep tracking of ordering process and generation info for the Ghost Kitchen. 

Sunny day scenarios: 
1. 

Extended use cases: 

Risks: 
1. What is the minimum time frame for ordering a meal that is not available in fridges, but can be prepared by Ghost Kitchen? 
2. Is it possible to make a mass order and set specific address? 
3. User ordered a meal but there is no possiblity to deliver it? Short of stock, kitchen closed. 

### Purchasing system 

Facade for payment systems

Sunny day scenarios: 

Extended use cases: 

Risks: 

### User applications

UI for the Ordering system

Sunny day scenarios: 

Extended use cases: 

Risks: 

### Integration between internal systems

Communication with upstream and downstream systems. 

Sunny day scenarios: 

Extended use cases: 

Risks: 

### Notification system

Make user informed on postponed in time actions. 

Sunny day scenarios: 
1. Default notification channel is in-app messages.

Extended use cases: 
1. User can setup preffered way of notification: in-app, push, email, sms
2. Notifications deffers by type an have different delivery channels. Types are: order related, news, feedback request, other. 

Risks: 
1. Should be there backup channel? 
2. Several ways of delivery for the same type? 

