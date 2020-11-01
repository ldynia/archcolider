# System approach 

## Design Desicions 

### Service-oriented approach 

The main proposal is to go with a quite big services that will help to develop, test, and deploy main logical parts independently. Identified services share common Quality Attributes, so the same set of Tactics can be applied. All those activities pointed to reduce time-to-market. 

![](https://github.com/ldynia/archcolider/blob/master/img/FF_Overview_v1.PNG)

### Modularized services 

Important decision here is to isolate communication between internal modules and make it as transparent as possible, pretending that there is the network connection. It also might looks as highly modularized monoliths.   

![](../img/FF_Modularization.PNG)

![](../img/FF_ModularizationExtraction.PNG)

### Event sourcing 

Event sourcing for order state management service (including payment tracker) provide confidence in history of changes for order and how it was paid. Orders by itself sensitive area that requires special attention with changes. Event sourcing helps reconstruct situations that led to error. Also, there is possibility to rebuild stack of events from the beginning with additional adjusting strategy. 

Rebuilding stack of events for domain entities might be handy in case of possible data migrations during active development phase. Not all requirements are known from the very beginning and we still want to have full history that can be used for analysis. 

![](https://github.com/ldynia/archcolider/blob/master/img/FF_OrdersAndScheduler.PNG)

### Log-based communication for information propagation between services 

Communication between services might be implemented in many ways. For service oriented approach there is an anti-pattern that we'd like to avoid: spaghetti with a meat-balls. We'd like to limit direct communication between services in case of updating supporting services like reporting or messaging. In fact, we was inspired by [M.Kleppmann talk](https://martin.kleppmann.com/2015/05/27/logs-for-data-infrastructure.html) about solving complexity with log-based streams. 

The main benefit that every service can consume data on it's own pace independently. It may reflexing requirements for availability and performance for some services, that will also allows to buy cheaper deployment instances for services. 

![](https://github.com/ldynia/archcolider/blob/master/img/FF_LogBasedStream.PNG)

### Health checks based on business critical path scenarious 

Monitoring is essential, but hardware\network metrics do not provide information about actual system availability. 

During Quality Atttibute Workshop those scenarios will be identified and listed in correspondent document. Critical path scenarious can be started by supervisor system and check correctness of a result and a time required for processing. Time measurement will show trends if there is a time to think about scaling in the appropriate from (up or out). 

### Independent data storage for reporting 

We'd like to secure performance and pressure to operational databases from the very beginning and plan reporting services accordingly. Too often reporting works on the same data storage as operational database. Information policies can dictate to store information for 3-5 and more years, usually it just left in operational database that decrease perfomance and makes migrations very hard. 

In this solution reporting service build it's own data storage with clear separation on operational and archived data to secure reports execution time. Implementation part touches: 
- data collection from log stream 
- map events to read-models for reporting engine
- execution retention policies for stored data

There is no sense to build in-house reporting service and the good option might be Tableau.

## Alternatives 

Number of alternatives that were rejected for now. 

### Microservices from the start 

Microservice approach requires a lot of attention to infrastructure, separation of responsibility, preferably stable and known domain model. For the _ordering system_ it's not applicable and developers effort will be wasted for invisible for end users things. 

Microservices should grows naturally as need arise.

### Monolith 

This approach good for Prove of Concept approach and early stages of startup. Here we can see certain level of maturity, so pure monolith would be oversimplification.

## Composition of components 

![Solution overview](../img/FF_Overview_v1.PNG)

*Gravity centers highlighted*

**Aim for Simplicity**

We'd like to provide initial simplicity for the overall system but that do not close the window for further extraction of services and independent development and deployment.

Grouping functional areas to benefit from ease of development and deployment

**Aim for Modifiability**

The second important part is to provide points of extensions and ease of modifiability for proposed solution. It means subparts can be extracted and extended without heavy refactoring.

### Composition 

- Point of Sale and Front End apps might be a single or two different applications that reuses the same UI elements and logic as it have much in common and opertator of PoS version impesonate other users in the system and follows the same workflow. 
- Feedback, Loyalty (Promotion/Discount), Menu catalog, Meal pickup - works with order composition and apply different "effects" on it, so for simplicity of development and deployment might be developed as modules of monolith to speed up development. But communictation between modules described in a such way that every module can be extracted as service in short time. Menu Catalog highlighted to show focal point of this composition. 
- Ordering and Scheduling - serves proper handling of orders and it make sense to implement it as separate subsystem from the very beginning. Ordering here is the focal point as it responsible for the lion share of operations and data consistency. 
- Purchase subsystem responsible for communication with payment providers or payment systems. It act as facade to payments system and handle all nuances of payment system usage. 
- Reporting - reporing engine and historical data for reports. Reports runs on dedicated historical storage to avoid influence on operational data storages. Also, it allows apply effective strategies for data archiving. 
- Notifications - facade for notification systems that will be used. For instance, sending notificatons by SMS, emails or in-app push notifications. 
- Payment systems, Ghost Kitchen, Smart-Fridge Management - external systems with which the _ordering system_ communicates but have no control. 

### Communication and security 

- Secured communication channels between all subsystems and modules. 
- Attribute based access control introduced from the beginning for all modules. 
- Integration with 3rd party identity providers is optional, but might be handy in terms of user engagement to avoid creating another one account. But an option to create independent account should remain for users who concerned about using accounts from tech giants. 

## COTS 

### Event Store 

Event sourcing is a technique that can be implemented with a variety of tools and approaches. Most of them have significant overhead in supporting sync between write and read models. Luckely there is EventStore project that can do boring stuff for us. We can start with OSS version and migrate then to SaaS. [ADR 009](https://github.com/ldynia/archcolider/blob/master/4.ADRs/009%20Event%20sourcing%20usage.md)

### Kafka 

The most known and widely supported tool for log streaming. Not much options to choose from, even if it is exceed current need in terms of performance and other provided features. 

### RabbitMQ

We decided to user RabbitmMQ as a messaging broker because it allows for at least once message delivery and provides message acknowledgement option. Furthermore, it's a widely used messaging solution in the IT community, with huge support for various programming languages and excellent tutorials. Based on various messaging tools comparation it allows for transactions, and build-in message persistence.

### DataDog vs Graphana vs ELK

Datadog is monitoring service for cloud-scale applications, providing monitoring of servers, databases, tools, and services, through a SaaS-based Cheap subscription base platform. Because it's easily integratable, and for a low monetary value we have huge technical gain in the subject of monitoring and tracking we decided to go with DataDog. Alternatives, that were trying to consider was Graphana and ELK stack but both of them required maintenance by developers, where DataDog is SaaS-base maintenance in offloaded form developers.

### Tableau Vs Power BI tools Vs koolreport

Tableau is preferred , because its easily integratable tool.
Power BI tools can be used if Business owner has a Microsoft Subscription.
KoolReport is an intuitive and flexible Open-Source PHP Reporting Framework for faster and easier report delivery.

## Missed topics 

- Security
- Local compliance with user privacy 
