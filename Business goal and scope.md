# The business goal: 

- A “ghost kitchen” (food preparation and cooking facility set up for the preparation of delivery-only meals.) needs an ordering system to allow users to have visibility of what items are available, purchase, and pick up items at any one of their points of sale / smart-fridge.

From the business goal definition we can briefly identify following areas of interests (subdomains):

Generic parts: 
1. Ordering system 
1. Purchasing system 

Context aware:
1. Reservation of food
1. Picking up food 
1. Point Of Sales integration with Ordering system 
1. Food catalog (visibility of items)

# Background: 

Company provide service for advicing and managing health nutrition for adult person (18-65 y.o. kids are in plans, but not in focus for now). Clients can subscribe for the service and get food according to their individual prescription. There are several distribution channels, and one of them is the smart-fridges. 

2 first locations in Detroit and 8 by 2021. 

## Smart-fridges capabilities 

Smart-fridges is like a food/drink kiosks that you can meet everywhere, but they are connected to company's backoffice. They have independent system and API. 

### Random 

1. In some point in time all that staff might be integrated with smart devices. But it requires a serious work with user's personal data. 
1. Fridges linkage - not thought about that, but it might be the case. Modularized system support. 
1. Send new meal request to a 3rd party kitchen -Send inventory updates to central kitchen

### Purchasing 

Via web-site and dedicated mobile application. 

### Authentication 

Currently by credit\debt card. User just swaping card and kiosk understand who is it. Auth based on last used card or pool of cards that are added to application. 

### Ordering 

1. Users should be able to make a personalized order upfront and get it later. In future plans, users should be able to browse entire catalog of available meals in fridges around them and order it. 
2. User should able "book" something if it is an open selling position. 
3. There might be option of setting pick-up time and notification that your meal arrived to a specific fridge. 
1. Collecting by proxy
4. Non-subscribers can use smart-fridges as well

## Numbers/Metrics (93m)

1. Currently 300 meals/week, plans to be 1500-2000 meals/week by december 
1. 68 locations by end of year 
1. 1000 subscribers by EoY  
1. 10 meals/week from subscriber 

## User communication / interacton 

1. Web application, site 
1. Push notifications 
1. Pickin' up on behalf of someone 
1. Feedback rewards model 
1. Discounts for users 

# Out of scope

1. Developing communication between smart-fridges internally and with the rest of the system 
1. Any logistics task related to delivery of the food. We accept that it is somehow delivered and unused food somehow removed from fridges. Also we don't care about any possible relocations of food. All food movements not caused by customer is out of scope.














