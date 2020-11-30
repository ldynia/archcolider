# Group Introduction

Good morning, Good afternoon and Good evening EVERYONE! ArchColider is a group of geeks whose members hold 4 different nationalities from two different continents. Despite cultural differences we share the same passion for software development, we believe in self-improvement and we would like to leave software a.k.a. world refactored. The final things that we have in common which allowed us to work efficiently was GMT+1 timezone, patient spouses, and kids who are asleep around 9pm. 

The name ArchColider was inspired by CERN’s Large Hydron Collider (the geekiest thing that we know). We feared that colliding our thoughts and experiences will give birth to a new architecture that would assemble Service Oriented MonstroLith (hahaha). Can you imagine our faces when we got the news that we were going to the semi-finals :) We are thrilled to present our solution and share it with you.

# Bussines Goal
Farmacy Food is a startup that aims to create tasty meals around peoples’ dietary needs. Farmacy food wishes to provide meals that are radically affordable and accessible. In order to do that Framacy Food has to collaborate with several stakeholders, including ghost kitchens (kitchen who cook the meals), point of sales (kiosk that holds smart fridges) and have a means to deliver meals to the smart fridge. It’s obvious that a startup needs software that will enable them grow. Like any startup it forecasts its user base, and has limited budget. The role of architect is to provide a solution that will respect business constraints and provide a solution that will allow Farmacy Food to achieve its goals.

# Presentation

We are ArchColider and this is our architectural proposal for Farmacy Food.

Farmacy Food is in a need of an ordering system that will connect its users with ghost kitchens. Based on startup requirements, we identified business drivers that guided us through designing architecture.

Furthermore, we have the following global assumptions about the IT landscape. We assume that smart fridges and ghost kitchen systems already have API, and can communicate with them. Additionally, we assume the ghost kitchen operates during regular working hours, not 24h per 7. Finally, the development team is small but experienced.

Requirements and assumptions lead us to constraint and scope, and more importantly, what is out of scope. No extensions or modification of smart fridges or ghost kitchen systems.

Significant Architectural Drivers (SAD) usually make a budget and architects SAD :(, because it shows the amount of necessary work. Requirements traceability is key!

We remember about stakeholders, developers, food suppliers and what they care about!

Moving to the solution. The domain area is sophisticated, and we decided to use a domain-driven approach to handle complexity. Not all parts of the system are equally important, so we need to know what we build or buy.

Conceptual Map helps validate business scenarios and connections between entities. Rules connected to knowledge level proves that the system keeps its logical integrity. Also, it helps to think about future possible business cases that do not exist now. An example of a case for promotion campaigned based on meal type.

From the technical perspective, we offer a modularized monolith - a set of them. The center of functional gravity are Meal Catalog and Ordering modules.

To start thinking about the next architectural patterns, we need to identify quality attributes. Simplicity and Modifiability are dominating qualities across the system.  Remember constraints?

However, every subsystem has its own quality attributes. It helps to pick patterns based on the specific needs of a subsystem.

To address modifiability and extensibility, we’ll use commands and events for communication between logical parts in monolith. Doing so, we’ll ensure that extraction of modules won’t be so painful as commands and events should flow as before.

If everything is done right – then extraction should be easy with communication and security checks in place.

All decisions about extracting or scaling services are based on facts. Metrics trend analysis should be used as fitness functions.

Conceptual map and quality attribute mapping help a lot in deciding information flow.

Potentially risky situation with concurrent updates of available meals, but the catalog should keep data consistency.
We propose to use the actor pattern because we have natural actors in life - fridges. A user always buys from a specific fridge, and a meal can’t magically jump from one fridge to another.

To avoid concurrency issues on the system level, we propose to use log-based streaming software. Someone said Kafka?

Infrastructure view allows us to understand the cost of the solution. First we suggest to scale up - it’ll be cheaper and faster as the system's load is small at the beginning. Then we can use metrics to make decisions.

Solution supports Farmacy Food accounts and the ability to use 3rd party providers.

Cost analysis might raise questions about the need for services. Still, ADRs should have answers or open discussions with owners about possible solutions.

Having a list of technical risks is good. Even better, is to have a list of business related risks. Because a variety of solutions is broad, and only the owner can decide how to handle risk.

The same with sensitive points. Review bombing is unanticipated but possible.
