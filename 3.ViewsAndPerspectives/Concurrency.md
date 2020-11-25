# Concurrency view

Describes the concurrency structure of the system and maps functional elements to concurrency units to clearly identify the parts of the system that can execute concurrently and how this is coordinated and controlled.

The Concurrency view is used to describe the system’s concurrency and state-related structure and constraints. This involves defining the parts of the system that can run at the same time and how this is to be controlled, by defining how the system’s functional elements are packaged into operating system processes and how the processes coordinate their execution

## Cases 

### Meal catalog integrity for available meals

_Add image_

The general sensitive points that we can identify here are:
- Update local catalog for users
- Update central catalog with user's data
- Update central catalog with kitchen data

**Update local catalog for users.**

Central catalog updates based on users orders and should be as actual as possible. We rely on backend data consistency and integrity as data from Ghost Kitchen and Smart Fridges unreliable and update frequency is unknown for the time of architecture modeling. We assume that data from Fridges comes once per X minute and we don't expect streaming interfaces for keeping catalog updated.

**Central Menu Catalog update**

Ghost kitchen provide updates once-twice per day as meals were released to fridges. So we get this data and update  data in catalog by adding amount of released meals.

Users orders subtract from available amount of tracked meals on backend.

Additional concerns raised when we'll have several instances of menu catalog in the system, but we going to address it by splitting menu catalog by geo area. It will help keep catalog small and consistence within area (city).

The main sensitive point comes from concurrent user's updates and we should solve it. One of solutions might be processing orders with actors model. Actor per fridge helps keep integrity of available amount of meals available in certain fridge.

QUESTIONS:

- We don't know what data provided from fridges: is it total amount of meals or delta. We hope for total amount.

RISKS:
- A lot of users in area and a need to calculate available meals in venue. Venue can have several fridges. There should be a model how to handle this
- A huge complexity in the system if Smart Fridge system do not sum availability of meals in specific venue. Most probably there is no such feature and fridges just share same location. Then we have to implement it on our own.


### Order porecessing on the back end

One of concerns that might arise for developers that never worked before with event sourcing system how to handle multiple simultanuously arriving orders? Will be there race conditions, deadlocks and other nasty things? 

Based on proposed architecture approach developers can recognize actor pattern and it means that orders processing one by one passed from one actor to another. Each actor can enrich emited event with additional information and keep internal state in a correct state. 

For instance, substructing meal amount from available stock happens in one actor and then a new event created and passed to the _Ordering system_. Actor connected with a meal catalog has only one simple responsibility and can processing events very fast. Taking into account nature of the business, we could say that there will be actors per fridge that have logical representation in our system. Users will order meals from a specific fridge, not from some random magic place that has all meals at once. 

The ordering system in turn checks possibility of payment charging and other things, and do it in the same manner with a help of a message queue system. When purchase confirmed fridge actor can safely ignore the message as deduction happens, or increase value of available meals for a particular fridge. 

Events about purchase published to log-based streaming system and a part that is responsible for providing info about overall availability can listen for events and update internal state accordingly without race conditions and locks. 

_add image here_

**Order processing** - sensitive point. We concerned about processing speed as we expect to work with time limitation for order processing. Ordering module process order (could check integrity) and send event to Payment Tracker, that should resend data to external Payment processor. Looks fine for a first iteration as we don't expect thousands of request per minute during first year-two. No need to update any data that used by several services. 

Having multiple readers for the order queue is safe there are messages about event (something that already happened). The main idea behind is that there might be multiple queues based on geo areas (cities or districts) that will speed up processing.  

**Scheduling** safe as it read data and can work on it's own pace. Ghost kitchen do not require real time updates as it prepares food for the one/two days upfront and need information about refill only.

### Promotional campaigns  

We don't expect any issues with promotions, as it's one way updates from central part and user's don't have any influence on this. We don't expect promotions based on overall amount of sold menu items. 

From the operators persective we don't want make it complicated right now involving CRDT (Conflict-free replicated data types) as campaigns do not changes often and there won't be dozens of operators. Preparing compaigns in Google Spreadsheet or Office365 Excel do the trick. We going to consume only final result without providing tools for creation and modifying withing designed system. 

### Other subsystems

Other parts of the system should consume data from log-based streaming and they'll get all messages in some order and can process them without locks. Those system might require internal load balancers\routers if number of messages is huge. But still it's easy to implement as messages should contain all necessary information for processing. 

## Checklist for further work 

- Is there a clear system-level concurrency model?
- Are your models at the right level of abstraction? Have you focused on the architecturally significant aspects?
- Can you simplify your concurrency design?
- Do all interested parties understand the overall concurrency strategy?
- Have you mapped all functional elements to a process (and thread if necessary)?
- Do you have a state model for at least one functional element in each process and thread? If not, are you sure the processes and threads will interact safely?
- Have you defined a suitable set of interprocess communication mechanisms to support the interelement interactions defined in the Functional view?
- Are all shared resources protected from corruption?
- Have you minimized the intertask communication and synchronization required?
- Do you have any resource hot spots in your system? If so, have you estimated the likely throughput, and is it high enough? Do you know how you would reduce contention at these points if forced to later?
- Can the system possibly deadlock? If so, do you have a strategy for recognizing and dealing with this when it occurs?
