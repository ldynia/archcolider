# The Business Goal: 

*A “ghost kitchen” (food preparation and cooking facility set up for the preparation of delivery-only meals.) needs an ordering system to allow users to have visibility of what items are available, purchase, and pick up items at any one of their points of sale / smart-fridge.*

From the business goal definition we can briefly identify following areas of interests:

**Core parts:**
1. Ordering system - tracking the process of ordering 
1. Food catalog - availability of items
1. Reservation of food 
1. Picking up food
1. Point Of Sales - integration with ordering system
1. Promotions and discounts

**Support** 
1. Feedbacks
1. User management

**Generic**
1. Payments 
1. Notifications

## Background: 

Company provide service for advising and managing health nutrition for adult person (18-65 y.o. kids are in plans, but not in focus for now). Clients can subscribe for the service and get food according to their individual nutritional needs (prescription). There are several distribution channels, and one of them is the smart-fridges. 

First two locations in Detroit, forecast of growth to eight by 2021. 

## Smart-fridges capabilities 

[Smart-fridge](https://github.com/ldynia/archcolider/blob/master/docs/PRESENTATION%20-%20Design%20and%20Analysis%20of%20Software%20Architectures%20PDF%20Ver.pdf) is like a food/drink kiosks that you can mount everywhere, it's connected to company's backoffice. They have independent system and API. 

## Purchasing 

Via web-site and dedicated mobile application.

## Authentication 

User authenticates with credit/debt card. User swaps the card and kiosk understand who he is. Authentication based on last used card or pool of cards that are added to application. 

## Ordering 

1. Users should be able to make a personalized order upfront and get it later. In future, users should be able to browse catalog of available meals in fridges close to him and order it. 
2. User should be able to "book" something if it is an open selling position. 
3. There might be option of setting pick-up time and notification that your meal arrived to a specific fridge. 
1. Collecting by proxies.
4. Non-subscribe users can use smart-fridges as well.

## User communication / interacton 

1. Web application (website) 
1. Push notifications 
1. Picking up on behalf of someone (proxy) 
1. Feedback rewards, surveys smodel 
1. Discounts for users 

## Numbers/Metrics ([93 minutes](https://learning.oreilly.com/live-training/courses/architectural-katas/0636920458463/))

1. Currently 300 meals/week, plans to be 1500-2000 meals/week by december 
1. 68 locations by end of year 
1. 1000 subscribers by EoY  
1. 10 meals/week from subscriber 

## Out of scope

1. Developing communication between smart-fridges internally and with the rest of the system.
1. Any logistics task related to delivery of the food. We accept that it is somehow delivered and unused food somehow removed from fridges. Also we don't care about any possible relocations of food. All food movements not caused by customer is out of scope.

## Random 

1. At some point in time, all that staff might be integrated with smart devices. But it requires a serious work with user's personal data. 
1. Fridges linkage, modularized system support -don't think about that
1. Send new meal request to a 3rd party kitchen 
1. Send inventory updates to central kitchen
