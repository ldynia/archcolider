# Risks 

## Business related risks 

1. The catalog is stale, and reserved food can't be dispatched from the selected smart-fridge. 
    - Option: Sync available items at purchase time to avoid reputational damages. 
2. Subscriber's menu can't be prepared. 
    - Options: Inform as soon as possible. Provide other meals from the same category. Add bonus coupons.  
3. Notification about delivery or meal can't be delivered by preferred channel. 
    - Option 1: Delivery via backup communication channels.
    - Option 2: Do nothing if meal arrived at the point of dispatching.
    - Option 3: If meal didn't arrive, then create a dedicated offer through PoS.
4. PoS app disconnected from the network. 
    - Option 1: Eventual consistency of operations. Send data when the network is available. 
    - Option 2: Pin codes to grab a meal from Subscriber
5. Smart fridge disconnected from the network. 
    - Option 1: Generate pin code for dispatching as soon as possible so the fridge and user's app will have it upfront. Possibly a few days upfront.  
6. User booked a meal, but not picked up. 
    - Option: prepay to accomplish the operation.
7. Meal is stuck in the fridge. 
    - Options: User takes a photo and files a complaint.

## Technical Risks 

1. Payment provider's service is temporarily down.
    - Options: All order records stored and requests to the payment system can be retried for a defined period of time. Trust policy for known users and subscribers. 
2. Spawining too many service instances lead to money wastes. 
    - Option 1: Configured maximum possible number of instances for each service
    - Option 2: Safety threshold, for instance, spawning, then confirmation from a system administrator. 
3. Ghost Kitchen is down and does not provide information about meals availability
    - Option 1: Business as usual using the _ordering system_ internal information. In case of dispatching fail use compensation protocol. 
4. Not applying security practices. 
    - Option: Involve 3rd party white hat hackers to scan for vulnerabilities. 
5. Risky releases with significant changes. 
    - Option 1: Enable hot-swap for previous releases. Set requirements for platform provider. 
6. Breaking changes in message formats for internal or external services.  
    - Option 1: Back and forward compatibility serialization formats of messages. 
    - Option 2: Keep at least 1 backward compatibility conversion mechanism. API versioning.
    - Option 3: Early negotiation with "sunset" header attribute and alerts for such header.
7. Mismatch of production and development environment
    - Option 1: Negotiation of 1:1 problem. I.e. run in dev the same set of infrastructure elements: at least 1 item for purely infrastructure related services (proxies, firewalls, load balancers) and at least 2 instances for business-related services (even if in prod there is only one). It help to identify many issues early.  

# Sensitive points 

## Business related 

1. Subscribers and Known users make an overprovisioning situation for a fridge. Not all food can be placed in a fridge. 
    - Option: _Need decision from the business on how to handle this situation_. 
2. Order was placed during off hours of Ghost Kitchen. 
3. Review bombing for a 3rd party kitchens.
    - Option: Review for service or meals available only for confirmed purchases. 

## Technical 

1. Modern cloud scaling technologies allows scaling up for a long time that might postpone decisions about scaling out. 
    - Business-critical path scenario evaluation on production 
2. Service overloading
    - Proactive monitoring
    - Circuit breaker 
    - Dog Pile protection 
 
    


