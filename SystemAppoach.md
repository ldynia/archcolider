# System approach 

_Style, principles, patterns, design decisions_

## Principles

1. Strive for cognitive simplicity 
2. Extensibility and modifiability preferred in case of trade-offs  
3. Telemetry is mandatory
4. Messages over direct calls

## Style

Based on provided principles, the system should be n-tier with layered approach within modules that secure functionality's extensibility. We can imagine it as a set of micro-kernels for each subdomain that communicates by messages (commands and events). Based on current [business goals](https://github.com/ldynia/archcolider/blob/master/Business%20goal%20and%20scope.md) (number of users, functionality current and desired) and [constraints](https://github.com/ldynia/archcolider/blob/master/Constraints.md) the primary implementation style of architecture is **modularized monolith**, with an accent to hight modularity to lower cost of further extractions to independent services. 

According to declared principles, we propose building systems based on event sourcing and domain-driven design for core components. 
- Event sourcing helps to trace and to reason about changes in domain models. It's necessary because many externals users are involved, and the system should provide a detailed investigation of every possible complaint from users about decision making, payment process, and overall awareness. 
- Domain-Driven Design (DDD) helps to control the cognitive complexity of the subject area where necessary. Even if starting implementation requires more effort than a transaction script approach or table-based, it will save a lot of time in the future. DDD also supports declared principles of cognitive simplicity and modifiability of the designed system.  

All subdomains should provide rich telemetry of usage to make an informative decision about extraction and next scaling if a component becomes a bottleneck for the solution. 

## Strategic domain design 

![Strategic Domain Design](/img/FF_StrategicDomainDesign.jpg)

In the image above, we present our vision of responsibilities for primary system contexts. 

**Core** 

The main differentiator of the business, unique modules that support business processes. In our case, there are: 
- Meal Catalog - A unique way of showing information about the meal, availability in fridges, ingredients. Also, information about promo actions, reviews, and so on accumulated here. 
- Ordering - A standard catering system might not help here as we need rich extensibility and control over orders. Subscribed orders, checking through online payment systems, using coupons and promo-actions, and feedback system only for confirmed buyers - it will be much easier to support with bespoke software. 
- Loyalty - There are unique ways of engaging new users, and limitations from other vendors should not tie the system owners. 

**Supportive**

Significant for business, but 3rd party tools may close the feature gap with proper customization or integration. 
- Feedback - The system should be highly extensible and might include survey mechanisms from other vendors.  The module provides a convenient way to manage feedback channels. 
- Scheduling helps to work with recurrent events from the Core areas and form the Ghost Kitchen orders. 

**Generic**

No or small customization is required for modules that fall into this basket—all needs covered in products available on the market. 
- Reporting - No need to implement a custom reporting engine as many specialized products can produce all necessary reports based on provided data. -
- Payments - We will only build a gateway to payment systems or even pick a payment provider to handle all specific communications with payment systems. 
- Notifications - It's better to use ready-made services that provide it to save time and money required for custom implementation. 

## Conceptual Model

Based on system description and requirements we build the conceptual model of 

![Metamodel](/img/FF_Metamodel.jpg)
