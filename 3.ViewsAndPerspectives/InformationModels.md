# Information models 

Our proposal for the architecture based on event sourcing, messaging and further decoupling of modules from monoliths. Thus, we don't see a value to provide relational based diagram with entities and links between them. Instead we can provide size estimation for main entities and frequency of events. Based on this information we can calculate required storage space and network bandwith estimation with forecasts for system growth.  

The following cases represents the most important parts for a early stage of application.  

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

#### Lifetime concerns 

- **The meal Catalog** lives around 24 hours or less on user's device and then should be forced to update 
- **History of orders** on local device might live around month to provide ability of fast reordering. Scheduled orders should have the same life span. 
- **Notifications** about meal ordering lives around 24 hours 
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

#### Lifetime concerns 

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

#### Lifetime concerns 

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

#### Lifetime concerns 

## Estimations of usage and costs

## Backup concerns 

- We don't need to backup data for orders in MQ, as the client app should implement a timeout mechanism for sending requests and getting responses. If there is no confirmation about payment acceptance or rejection, a user should be notified and retry should be offered. So for MQ we can rely on the build-in persistence model for the service restart scenario.
- EventStore requires a backup mechanism as it vital information for the system. Projections do not require backup as they can be reconstructed from events in EventStore. But we can backup projections to speedup the recovery scenario.
- Report service requires backup mechanism.
- Kafka do not require and we can rely on a build-in mechanisms.




