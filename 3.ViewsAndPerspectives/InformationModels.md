# Information models 

Our proposal for the architecture based on event sourcing, messaging and further decoupling of modules from monoliths. Thus, we don't see a value to provide relational based diagram with entities and links between them. Instead we can provide size estimation for main entities and frequency of events. Based on this information we can calculate required storage space and network bandwith estimation with forecasts for system growth.  

The following cases represents the most important parts for a early stage of application.  

## General considerations 

One of the biggest advantages for the whole data management process is geo separation. Almost everything might be sharder based on geo-locations of users and fridges. Every big enough geo district (city district, city, suburbane area) will have it's own shard of data that don't require any replication anywhere. Ghost kitchen in Detroit won't offer meals in the New-York City. User's traveling all the time, but their past orders not. In each new area there would be the unique set of preferences according to a presented ghost kitchens. Only a fairly small amount of data need to be accessed in any location, like payment information. This basic idea and assumption simplify overall data model in terms of access, replication, modifying and so on.   

## Cases 

### Client application 

Here under client application we understand mobile application and point of sale app, as they behave on conceptual level identically and require the same events and data. 

_Why is it important?_ 

The application is the main communication channel and the process of catalog browsing and purchasing should be fast and reliable from user's perspective. Access to past data related to a user should be smooth as well. 

Slow working application disenurage users from using it and do any purchases as there fear that payment information might be lost, order double charged and so on. 

#### Stakeholders concerns 

| Stakeholder | Conserns | 
|---------|------| 
| Subscriber | Get information about upcoming order according to a schedule | 
| | Ability to modify (change\cancel) scheduled menu |
| Known users | Browse catalog with no delay and see meals availability in fridges for selected area | 
| | Purchase and reserve meal | 
|  | Executing purchase with minimum clicks in interface |
| Ocassional users | Get information about nutrition facts for selected meal | 
| | Buy selected meal without significant delay waiting data about meal availability\reservation | 
| Pos Admins | Executing purchase with minimum clicks in interface | 
| Developers | Data models simplicity | 

#### Diagrams 

**Meal stock updates** 

The main accent here is how data on client's devices will be updated and information about available meals can be kept up to date. Based on the diagram and the business model updates might be sent to users based on their location. Location might updates every time when user opens application. 

![](../img/IM_meal_stock_update.PNG)

On the image above you can see order of events/commands. It represents how a client app get updates about offered meals and amount of meals in stock. 

| Event\Command\Queries | Description | Frequency | Size (kb)  | 
|-------|-----|--------|---|
| Catalog Updated | Event that notify client app that catalog have changes in meals offering. Note, that Smart fridges publish the same event. Even if it's not true from thechnical point of view, our ACL can transform data from fridges to this event to unify overall processing | Most probably once per day per user | 0,1 | 
| Meal Stock Updated | Contains information about a meal and remain amount in stock  | With every placed order. Batch update from Smart Fridges. Delivery might be optimized by user's location. | 0,1-150 |
| Meal Stock Reserved | Let know the Catalog that meal soon will be reserved. Helps manage amount of meals in stock  | With every placed order | 0,1 |
| Get Catalog (query) | Reference to a specific catalog or all of available catalogs in the user's area | Every time when user starts forming new order. 1-2 times per day by schedule | 0,1/150-300 (without images) | 
| Confirm Order by User | Command that send user's intention to order a meal | Every time when user finish order composing and going to pay | 0,2 | 

TRADE-OFFS:
- _CatalogUpdated_ might have information about the update, such as a new meal description, ingridients and so on. It seems to be a nice aproach as it "push" model and clients get all necessary information without a need to callback backend for an additional information. From other hand, not all clients might be reachable and process the data. Also there are might be several catalogs and push updates to a client with entire catalog might be not necessary, as client can have preference for a certain meal catalog. The most reasonable way might be just inform about the fact of update, catalog name/id, location. 

**Meal purchase** 

![](../img/IM_meal_purchase.PNG)

On the diagram represented sunny day scenario in a simplified way to represent how order information flows throwgh the system and how user got responce about purchase. Coupon checks is ommited, as it's bonus feature =) This case tightly coupled with a previous one about stock change propagation. 

| Event\Command\Queries | Description | Frequency | Size (kb)  | 
|-------|-----|--------|---|
| Start Order | Self-descriptive :) Just preapre a place holder for a new order. Nothing bother backend. | We don't care as it local command | N/A | 
| Apply Coupon | User apply code and we don't care yet what the code is | We don't care as it local command | N/A | 
| Confirm Order by User | User confirms that order if formed and it's sign for a local app, that the order should be sent to the backend for processing | Every time when user finish order composing and going to pay. 1-3 time per day per user (except subscribers) | 0,2 | 
| Purchase Order | Order system checks that the order can be technicaly delivered (i.e. there are sufficient amount of meals in a fridge) and the payment system should confirm actual purchase |  1-3 time per day per user (except subscribers) | 0,2 | 
| Order Purchase Confirmed | Self-explained | Once per order normally | 0,1 | 
| Meal Stock Updated | Catalog informed that the amount of meals changed. | With every confirmed order, and update from SmartFridges | 0,2 | 
| Order purchased | Confirmation for user and the client app that everything processed sucessfully and fridge, or ghost kitchen informed about user's desire | Once per order normally. | 0,1 | 

**Cancel order by user** 

![](../img/IM_cancel_order_by_user.PNG)

The story behind this diagram is that user can cancel any order, and as gmail do, we can inhibit order execution for a 10-30 seconds to give a chance for a user to cancel an order without any complications as refunding and involving payment systems. In common case, user get's notification about order processing as soon as backend get the command for making order. But then it's totally ok, to postpone any further actions for a some time as a purchase might be impulsive and immidiate cancelation could happen.  

The case when the payment system charged a user and there is a cancelation happened described in the next section. 

| Event\Command\Queries | Description | Frequency | Size (kb)  | 
|-------|-----|--------|---|
| Start Order | Self-descriptive :) Just preapre a place holder for a new order. Nothing bother backend. | We don't care as it local command | N/A | 
| Cancel order by user | We must take care about two major cases: 1) cancel order that wasn't confirmed yet. Then no impact on backend. 2) Request was sent, but then canceled. | 2%-5% of all orders | 0,1 | 
| Meal Stock Canceled | - | 2%-5% of all orders | 0,1 | 
| Meal Stock Updated | Catalog informed that the amount of meals changed. | With every confirmed order, and update from SmartFridges | 0,2 | 

**Cancel scheduled order by user** 

It's a normal situation when user prepaid for a some service and then can cancel it at any time. So we should represent it in our system as well, because "subscribers" is the target group for the Farmacy Food. So a _subscriber_ should 

![](../img/IM_cancel_scheduled_order_by_user.PNG)

One of important things here, that in case of cancelling scheduled orders, there is no impact on meals catalog, as user in general should cancel something that not exists. Refund process mainly is a technical concern, but there might be business aspects. So having _ClaimRefund_ command is nice, as we can process it in different ways based on business model. 

ASSUMPTIONS: 
- User can't cancel meals that was already produced and delivered. Cancelation is effective from the next business day. But it's business decision. Meals can be moved to a available-to-all-stock.  

RISKS: 
- Ghost kitchen prepare meals up to 3 days upfront according to a schedule. Probability is low, as FF strive for fresh and healthy food and (we hope) minimal wastes. 


#### Lifetime concerns 

We asume that following entities will be presented and stored on user's device. 

- **The meal Catalog** lives around 24 hours or less on user's device and then should be forced to update.
- **History of orders** on local device might live around month to provide ability of fast reordering. Scheduled orders should have the same life span. 
- **Notifications** about meal ordering lives around 24 hours.
- **Promo notifications** available during whole compaign or manual deleting.  

### Order processing on backend 

_Why is it important?_ 

Order processing (single purchases or scheduler orders) is a money maker part of the system. We'd like to review related parts and identify main moving parts, quaranties, sensitive points and other possible concerns. 

A clear model how it works helps to ease implementation process and address risks (business and techincal) earlier during system design.  

#### Stakeholders concerns 

| Stakeholder | Conserns | 
|---------|------| 
| All type of users | Accurate processing with a time fashioned feedback about purchase result | 
| Ghost kitchen | Information about upcoming orders | 
| Owner | Analytics about usage patterns | 


#### Diagrams 

Many aspects was touched on previous diagrams and at this stage of development we can refernce to them without changes. 

**Cancel scheduled order by payment system** 

![](../img/IM_cancel_order_by_payment_system.PNG)

The most interesing part here are events from the _System order_. The payment might be refused, or take so much time that it should be refused by timeout. In both cases user should be notified about a failure. 

The most important part here is to notify user that purchase failed. Then the backend should not store any operational information about the purchase, only reporting domian will know about failed attempt. User's app can handle _OrderPurchaseRefused_ as signal to retry the last order from the order history that stored locally. User just need to confirm a new attempt. 

**Preparing scheduled orders for subscribers** 

![](../img/IM_preparing_scheduled_orders.PNG)



TRADE-OFFS:
- Scheduled orders might be decomposed and created up front for the whole period of scheduling. Then it will bloat the order base and requires a special mark that can tell us when an order should be executed. It might be simplier in terms of order processing, as all necessary orders are in place. But it brings issues when schedule changes or cancels. Multiple updates requires. On other side, schedule might be a logical structure, according to which every day a new orders will be generated and processed. It will be much easier to handle changes in schedule, but introduce additional rules for payment processing part. Such orders should be marked as pre-paid. Might be solved with a special promo campaign "subscriber". 

#### Lifetime concerns 

We asume that following entities will be presented and stored on user's device. 

- **Order on backend** lives around 10-15 minutes, starting from the moment of reciving _order confirmation_. During timeframe setted business all operations related to purchase should be complited. If not, then reserve meal record dismissed and all concerned parts of the system get notification that order is unsuccessfull.   
- **History of orders** on local device might live around month to provide ability of fast reordering. Scheduled orders should have the same life span.   
- **Scheduled orders** presented for "scheduled" timeframe  



### Promotional compaigns 

_Why is it important?_

The one of business goals is to expand to other areas and convert ocassional users to subscribers. Promotional compaigns used wisely is a great leverage for user base growth and engage users to use application again and again. 

#### Stakeholders concerns 

| Stakeholder | Conserns | 
|---------|------| 
| All type of users | Ability to use compaign promotional materials | 
| Subscribers, Known Users | Information about bonus points and ability to use them | 
| Owner | Source for analytics about involvment, usage, bonus point spendings | 
| | Popularity of provided meals | 
| Admins of promo | Ease of creating and tracking compaigns | 

#### Diagrams 

TBD

#### Lifetime concerns 

TBD

### Amount of meals sold

_Why is it important?_

Blazingly fast application and brilliant promotional compaigns won't help if there is no information about in-stock meals so users could actually benefit from the app and promo. We should strive for providing as actual info about available meals in-stock as possible.  

Ghost kitchen (3rd party as well) could gain information about actually sold and picked up items (the first do not always implies the second). It might help them better plan production plan for the next day or two.  

#### Stakeholders concerns 

| Stakeholder | Conserns | 
|---------|------| 
| All type of users | Actual information about available meals to avoid disappointment when after some purchasing steps in the app there is notification about out-of-stock. |
| Owner | Increase the level of satisfaction for users | 
| Ghost kitchen | Information about actually sold and dispatched items  | 
| Developers | Avoid race conditions and unnecessary complexity in data updating |  

#### Diagrams 

**Meal purchase** 

(copy one of previous scenarios)

![](../img/IM_meal_purchase.PNG)

On the diagram represented sunny day scenario in a simplified way to represent how order information flows throwgh the system and how user got responce about purchase. Coupon checks is ommited, as it's bonus feature =) This case tightly coupled with a previous one about stock change propagation. 

| Event\Command\Queries | Description | Frequency | Size (kb)  | 
|-------|-----|--------|---|
| Start Order | Self-descriptive :) Just preapre a place holder for a new order. Nothing bother backend. | We don't care as it local command | N/A | 
| Apply Coupon | User apply code and we don't care yet what the code is | We don't care as it local command | N/A | 
| Confirm Order by User | User confirms that order if formed and it's sign for a local app, that the order should be sent to the backend for processing | Every time when user finish order composing and going to pay. 1-3 time per day per user (except subscribers) | 0,2 | 
| Purchase Order | Order system checks that the order can be technicaly delivered (i.e. there are sufficient amount of meals in a fridge) and the payment system should confirm actual purchase |  1-3 time per day per user (except subscribers) | 0,2 | 
| Order Purchase Confirmed | Self-explained | Once per order normally | 0,1 | 
| Meal Stock Updated | Catalog informed that the amount of meals changed. | With every confirmed order, and update from SmartFridges | 0,2 | 
| Order purchased | Confirmation for user and the client app that everything processed sucessfully and fridge, or ghost kitchen informed about user's desire | Once per order normally. | 0,1 | 

#### Lifetime concerns 

## Estimations of usage and costs

## Backup concerns 

- We don't need to backup data for orders in MQ, as the client app should implement a timeout mechanism for sending requests and getting responses. If there is no confirmation about payment acceptance or rejection, a user should be notified and retry should be offered. So for MQ we can rely on the build-in persistence model for the service restart scenario.
- EventStore requires a backup mechanism as it vital information for the system. Projections generated by EventStore do not require backup as they can be reconstructed from events in EventStore. But we can backup projections to speedup the recovery scenario.
- Report service requires backup mechanism to keep operational and historical data for analysis
- Kafka do not require additional backup mechanism on this stage and we can rely on a build-in mechanisms.




