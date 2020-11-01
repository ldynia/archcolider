# System overview

## Business goal 

Business goal declared by owner:

*A “ghost kitchen” (food preparation and cooking facility set up for the preparation of delivery-only meals.) needs an ordering system to allow users to have visibility of what items are available, purchase, and pick up items at any one of their points of sale / smart-fridge.*


## Background: 

Farmacy Food is a tech-enabled healthy food startup that takes the “Let food be thy medicine” quote literally and creates tasty meals around peoples’ dietary needs and active lifestyles to support their overall well-being. Our mission is to make health and wellness radically affordable and accessible.

Farmacy Food mission: https://www.youtube.com/watch?v=9aSLSVAIkoM

Farmacy Food website: https://www.farmacyfood.com/


Company provide service for advising and managing health nutrition for an adult person (18-65 y.o. kids are in plans, but not in focus for now). Clients can subscribe to the service and get food according to their individual nutritional needs (prescription). There are several distribution channels, and one of them is smart-fridges. 

First two locations in Detroit forecast of growth to eight by 2021. 

### Internal systems with which the system interacts

#### Smart-fridges  

[Smart-fridge](https://github.com/ldynia/archcolider/blob/master/docs/PRESENTATION%20-%20Design%20and%20Analysis%20of%20Software%20Architectures%20PDF%20Ver.pdf) is like a food/drink kiosks that you can mount everywhere; it’s connected to the company’s back-office. They have an independent system and API. 

#### Ghost Kitchen ordering system 

Ghost kitchen backoffice (https://pos.toasttab.com/) for managing food production. 

#### Point of sales 

Not clear how currently it works, but it supports sales in PoS for not registered users. 
The Kiosk is a sublet space inside another business where we will sell our product but have an employee handle the transactions through a point of sale. The same data should be accessible through the POS systems API’s


### Numbers/Metrics

1. Currently 300 meals/week, plans to be 1500-2000 meals/week by December 
1. 68 locations by the end of the year 
1. 1000 subscribers by EoY  
1. 10 meals/week from a subscriber 

## System features and responsibilities 

### Ghost kitchen 

1. Send inventory updates to the central ghost kitchen
1. Send new meal request to a 3rd party kitchen 

## Users

1. Mobile/Web application 
1. Users should be able to make a personalized order upfront and get it later. In the future, users should be able to browse the catalog of available meals in fridges close to them and order meals. 
2. User should be able to “book” something if it is an open selling position. 
3. There might be an option of setting pick-up time and notification that your meal arrived at a specific fridge. 
1. Collecting by proxies.
4. Non-subscribe users can use smart-fridges as well.
5. Rewards, coupons, promotions and other engagement activitiy.
6. The user authenticates with a credit/debit card. The user swaps the card, and a kiosk understands who is operating. Authentication is based on the last used card or pool of cards that are added to the application. 


### Other 

1. At some point in time, all that staff might be integrated with smart devices. But it requires serious work with user’s private data. 
1. Fridges linkage, modularized system support 


## Out of scope

1. Developing communication between smart-fridges internally and with the rest of the system.
1. Any logistics task related to the delivery of the food. We accept that it is somehow delivered, and unused food is somehow removed from fridges. Also, we don’t care about any possible relocations of food. All food movements not caused by a customer is out of scope.


