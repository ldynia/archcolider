# Solution overview

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

Based on system description and requirements, we build the conceptual model of the _ordering system_. 

![Metamodel](/img/FF_Metamodel_v1.png)

_Knowledge level_ describes rules how actors/entities interact with each other 
_Operational level_ describe main actors/entities involved in main scenarios 

Metamodel covers all existing business scenarios and should be capable of absorbing future ones. Even more, metamodel should encourage to think about new scenarios that open in a metamodel.  

Referring to the diagram: 

_User_ and _User type_ describes possible users that might interact with the system. On meta-level, Subscriber and PoS admin (or even PoS) has no difference. From an operational perspective, they are performing some _actions_ upon _order_. _Action types_ depends on _User type_ and those rules described on the knowledge level. Certainly, there are set of _action types_ that are common for all _user types_, and it might lead us to an idea of command implementation to share possibilities between _user types_ in convenient way. 

_Action types_ situated by _place_ where they performed, and, for instance, _PoS_ might perform some steps implicitly to move an _order_ to desired _order state_. 

_Order_ formed from a _menu_ that provided by _ghost kitchen_. There might be many _ghost kitchens_ with a variety of _menus_ which in turn consist of _meals_ that might be common for many _menus_. For the ease of navigation, management, filtering, and other actions all _meals_ described by its _meal type_. Any _meal_ might be described by a set of _meal types_. 

Depends on _order type_ and _order state_, there is a _scheduling_ strategy that serves reservation and recurrent orders. 

_Promotions_ applied to _menu_ and pointed out to a specific _meal_ or _meal types_. It was made intentionally because if _promotions_ is connected with _meals_, then it hard to set promotions that depend on _ghost kitchen_ (a possible scenario - that promotions provided by a specific _ghost kitchen_, not a platform in general). _Promotion type_ might be based on _feedback type_ as survey, review, but do not constraint to _feedback_, as _promotion_ can be applied to all users. At the same time, a connection between _promotion type_ and _feedback type_ allows the owner to build user engagement programs. 

Relation connection between _promotion type_ and _order type_ (and _order state_) offers a flexible mechanism of possible constraints for participation in promotion campaigns.  

## Component composition and communication 

![Solution overview](../img/FF_Overview_v1.PNG)

**Aim for Simplicity**

We'd like to provide initial simplicity for the overall system but that do not close the window for further extraction of services and independent development and deployment.

Grouping functional areas to benefit from ease of development and deployment

**Aim for Modifiability**

The second important part is to provide points of extensions and ease of modifiability for proposed solution. It means subparts can be extracted and extended without heavy refactoring.

### Composition 

- Point of Sale and Front End apps might be a single or two different applications that reuses the same UI elements and logic as it have much in common and opertator of PoS version impesonate other users in the system and follows the same workflow. 
- Feedback, Loyalty (Promotion/Discount), Menu catalog, Meal pickup - works with order composition and apply different "effects" on it, so for simplicity of development and deployment might be developed as modules of monolith to speed up development. But communictation between modules described in a such way that every module can be extracted as service in short time. Menu Catalog highlighted to show focal point of this composition. 
- Ordering and Scheduling - serves proper handling of orders and it make sense to implement it as separate subsystem from the very beginning. Ordering here is the focal point as it responsible for the lion share of operations and data consistency. 
- Purchase subsystem responsible for communication with payment providers or payment systems. 




