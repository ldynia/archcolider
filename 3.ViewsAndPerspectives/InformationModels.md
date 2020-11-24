# Information models 

Our proposal for the architecture based on event sourcing, messaging and further decoupling of modules from monoliths. Thus, we don't see a value to provide relational based diagram with entities and links between them. Instead we can provide size estimation for main entities and frequency of events. Based on this information we can calculate required storage space and network bandwith estimation with forecasts for system growth.  

The following cases represents the most important parts for a early stage of application.  

## Cases 

### Client application 

Here under client application we understand mobile application and point of sale app, as they behave on conceptual level identically and require the same events and data. 

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

| Stakeholder | Conserns | 
|---------|------| 
| All type of users | Accurate processing with a time fashioned feedback about purchase result | 
| Ghost kitchen | Information about upcoming orders | 
| Owner | Analytics about usage patterns | 

#### Stakeholders concerns 

#### Diagrams 

#### Lifetime concerns 

### Promotional compaigns 

| Stakeholder | Conserns | 
|---------|------| 
| All type of users | Ability to use compaign promotional materials | 
| Subscribers, Known Users | Information about bonus points and ability to use them | 
| Owner | Source for analytics about involvment, usage, bonus point spendings | 
| | Popularity of provided meals | 
| Admins of promo | Ease of creating and tracking | 

#### Stakeholders concerns 

#### Diagrams 

#### Lifetime concerns 

### Amount of meals  

| Stakeholder | Conserns | 
|---------|------| 
| All type of users | Actual information about available meals to avoid disappointment when after some purchasing steps in the app there is notification about out-of-stock. |
| Owner | Increase the level of satisfaction for users | 
| Ghost kitchen | Information about actually sold and dispatched items  | 
| Developers | Avoid race conditions and unnecessary complexity in data updating |  

#### Stakeholders concerns 

#### Diagrams 

#### Lifetime concerns 

## Estimations of usage and costs

## Backup concerns 

- We don't need to backup data for orders in MQ, as the client app should implement a timeout mechanism for sending requests and getting responses. If there is no confirmation about payment acceptance or rejection, a user should be notified and retry should be offered. So for MQ we can rely on the build-in persistence model for the service restart scenario.
- EventStore requires a backup mechanism as it vital information for the system. Projections do not require backup as they can be reconstructed from events in EventStore. But we can backup projections to speedup the recovery scenario.
- Report service requires backup mechanism.
- Kafka do not require and we can rely on a build-in mechanisms.




