# System approach 

## Design Decisions 

### Service-oriented approach 

The main proposal is to go with quite big services that will help to develop, test, and deploy the main logical parts independently. Identified services share common Quality Attributes, so the same set of Tactics can be applied. All those activities pointed to reduce time-to-market. 

![](https://github.com/ldynia/archcolider/blob/master/img/FF_Overview_v1.PNG)

As we propose modularised monolith with further modification to services, every part has it's own major quality attributes that have to be address first. But we'd like to point to overall system quality attributes as well, that should be addresed before anything else. 

#### System Quality Attributes

**Simplicity**

We'd like to provide initial simplicity for the overall system but that do not close the window for further extraction of services and independent development and deployment.

Grouping functional areas to benefit from ease of development and deployment

**Modifiability**

The second important part is to provide points of extensions and ease of modifiability for proposed solution. It means subparts can be extracted and extended without heavy refactoring.

#### Front-end apps 

**Usabitility**

Application should be easy to use for a wide range of users in different age groups. Entry level should be low. The meal catalog navigation should be easy and purchasing process is obvious. Application should guide users with major activities.  

**Performance**

Application should provide the main information with as low delays as possible. Network speed should not have impact on browsing the meal catalog and placing items in the basket. 

**Autonomous**

Compliment the Performance quality attribute and secure work of PoS in case of disconnection or high network latency.  

#### Meal Catalog subsystem

**Extensibility**

The meal catalog subsystem starts as modularized monolith and should support extensibility first to be able add features while overall system matures and the business model proves liveness. Extensibility not only responsible for adding new parts but also for extracting parts that become a big enought to live as independent service. 

**Maintainability**

The code base should follow good coding practices and use necesssary patterns to support extensibility first. Maintainability includes also tests, metrics, and healt checks to ease maintainability from coding and operational perspective. 

**Abvailability**

Without good availability there won't be cash flow so this is also important quality attribute. But we'd to note, that reader should not confuse it with surviveability as it's still prove of business model and serice restarting, short ouutage and so on in still possible but they should be solved with restarts and vertical scale. On later stages it might become more important and other architectural tactics will be involved. 

In general system should be available even if performance might degradate. 

#### Order Processing subsystem

**Reliability**

Transparency and accurate responses is the main theme for this service. User should be informed about status and result of purchase process. This quality attribute address user satisfaction requirement and keep user user and other system's parts informed about purchase process as it impact many other subsystems. 

**Integrity**

Data integrity is important when we talk about cash flow and informaton about order purchasing should be accurate to avoid double charges, lost payments and so on. Avoid corrupton of payment state is essential. 

#### Purchase gateway

**Security**

Payment data and operations should have the highest level of security as it impact on trustworthy of overall system. Sending sensitive payment information should be secured. Communitcation with payment providers should enforce this quality attribute as well. 

**Abvailability**

Inability to make payment cause direct money loses as the whole business based on selling goods. Payment requests should be processed with the highest priority and we should respect the will of customers spend money. No matter what but payment should be sent.

#### Reporting subsystem

**Reliability**

Reporting system is in support category and we should think about keeping history data. The main topic here is not to lose data as it valuable source of information for future business decisions.  

#### Notification subsystem

**Reliability**

Notification system also in support category and should make the subsystem relyable enougth to send notification to users. Notification sending provided by a platform, but should secure possibility of getting those notification event from the rest of the system.  

### Modularized services 

The important decision here is to isolate communication between internal modules and make it as transparent as possible, pretending that there is a network connection. It also might look like highly modularized monoliths.   

![](../img/FF_Modularization.PNG)

![](../img/FF_ModularizationExtraction.PNG)

### Event sourcing 

Event sourcing for order state management service (including payment tracker) provides confidence in the history of changes for order and how it was paid. Orders by itself is a sensitive area that requires special attention to changes. Event sourcing helps reconstruct situations that led to errors. Also, there is a possibility to rebuild the stack of events from the beginning with an additional adjusting strategy. 

Rebuilding a stack of events for domain entities might be handy in case of possible data migrations during the active development phase. Not all requirements are known from the very beginning, and we still want to have a full history that can be used for analysis. 

![](https://github.com/ldynia/archcolider/blob/master/img/FF_OrdersAndScheduler.PNG)

### Log-based communication for information propagation between services 

Communication between services might be implemented in many ways. There is an anti-pattern that we'd like to avoid for a service-oriented approach: spaghetti with meatballs. We'd like to limit direct communication between services in case of updating supporting services like reporting or messaging. In fact, we were inspired by [M. Kleppmann talk](https://martin.kleppmann.com/2015/05/27/logs-for-data-infrastructure.html) about solving complexity with log-based streams. 

The main benefit that every service can consume data at its own pace independently. It may relax requirements for availability and performance for some services that will also allow buying cheaper deployment instances. 

![](https://github.com/ldynia/archcolider/blob/master/img/FF_LogBasedStream.PNG)

### Health checks based on business-critical path scenarios 

Monitoring is essential, but hardware\network metrics do not provide information about actual system availability. 

During the Quality Attribute Workshop, those scenarios will be identified and listed in the corresponding document. Critical path scenarios can be started by a supervisor system and check the correctness of a result and a time required for processing. Time measurement will show trends if there is a time to think about scaling in the appropriate form (up or out). 

### Independent data storage for reporting 

We want to secure performance and pressure to an operational database from the very beginning and plan reporting services accordingly. Too often, reporting works on the same data storage as an operational database. Information policies can dictate to store information for 3-5 and more years, usually those data just left in the operational database that decreases performance and makes migrations very hard. 

In this solution reporting service build it's own data storage with clear separation on operational and archived data to secure reports execution time. Implementation part touches: 
- data collection from log stream 
- map events to read-models for reporting engine
- execution retention policies for stored data

There is no sense to build in-house reporting service, and the good option might be Apache Superset.

## Alternatives 

A number of alternatives that were rejected for now. 

### Microservices from the start 

Microservice approach requires a lot of attention to infrastructure, separation of responsibility, preferably a stable and known domain model. For the _ordering system_ it's not applicable, and developers effort will be wasted for invisible for end-users things. 

Microservices should grow naturally as the need arise.

### Monolith 

This approach is good for Proof of Concept approach and early stages of a startup. Here we can see a certain level of maturity, so pure monolith would be oversimplification.

## Composition of components 

![Solution overview](../img/FF_Overview_v1.PNG)

*Gravity centers highlighted*

**Aim for Simplicity**

We'd like to provide initial simplicity for the overall system but that does not close the window for further extraction of services and independent development and deployment.

Grouping functional areas to benefit from the ease of development and deployment.

**Aim for Modifiability**

The second important part is to provide points of extensions and ease of modifiability for the proposed solution. It means subparts can be extracted and extended without massive refactoring.

### Composition 

- Point of Sale and Front End apps might be a single or two different applications that reuse the same UI elements and logic as it has much in common, and operator of PoS version impersonate other users in the system and follows the same workflow. 
- Feedback, Loyalty (Promotion/Discount), Menu catalog, Meal pickup - works with order composition and apply different "effects" on it, so for simplicity of development and deployment might be developed as modules of a monolith to speed up development. But communication between modules described in such a way that every module can be extracted as a service in a short time. Menu Catalog highlighted to show the focal point of this composition. 
- Ordering and Scheduling - serves proper handling of orders, and it makes sense to implement it as a separate subsystem from the very beginning. Ordering here is the focal point as it is responsible for the lion share of operations and data consistency. 
- The purchase subsystem is responsible for communication with payment providers or payment systems. It acts as a facade to payments system and handles all nuances of payment system usage. 
- Reporting - reporting engine and historical data for reports. Reports run on dedicated historical storage to avoid influence on operational data storage. Also, it allows for applying effective strategies for data archiving. 
- Notifications - facade for notification systems that will be used. For instance, sending notifications by SMS, emails, or in-app push notifications. 
- Payment systems, Ghost Kitchen, Smart-Fridge Management - external systems with which the _ordering system_ communicates but have no control. 

### Communication and security 

- Secured communication channels between all subsystems and modules. 
- Attribute-based access control introduced from the beginning for all modules. 
- Integration with 3rd party identity providers is optional but might be handy in terms of user engagement to avoid creating another one account. But an option to create independent account should remain for users who are concerned about using accounts from tech giants. 

## COTS 

### Event Store 

Event sourcing is a technique that can be implemented with a variety of tools and approaches. Most of them have significant overhead in supporting sync between write and read models. Luckily there is EventStore project that can do boring stuff for us. We can start with OSS version and migrate then to SaaS. [ADR 009](https://github.com/ldynia/archcolider/blob/master/4.ADRs/009%20Event%20sourcing%20usage.md)

### Kafka 

The most known and widely supported tool for log streaming. Not many options to choose from, even if it exceeds current need in terms of performance and other provided features. 

### RabbitMQ

We decided to user RabbitmMQ as a messaging broker because it allows for at least once message delivery and provides a message acknowledgement option. Furthermore, it's a widely used messaging solution in the IT community, with huge support for various programming languages and excellent tutorials. Based on various messaging tools comparation it allows for transactions and build-in message persistence.

### DataDog vs Graphana vs ELK

Datadog is a monitoring service for cloud-scale applications, providing monitoring of servers, databases, tools, and services through a SaaS-based cheap subscription-based platform. Because it's easily integratable , and for a low monetary value, we have huge technical gain in the subject of monitoring and tracking, we decided to go with DataDog. Alternatives that were trying to consider was Graphana and ELK stack but both of them required maintenance by developers, where DataDog is SaaS-base maintenance in offloaded form developers.

### Tableau Vs Power BI tools Vs koolreport

Tableau is preferred , because of its easily integratable tool.
Power BI tools can be used if the Business owner has a Microsoft Subscription.
KoolReport is an intuitive and flexible Open-Source PHP Reporting Framework for faster and easier report delivery.

## Missed topics 

- Security
- Local compliance with user privacy 
