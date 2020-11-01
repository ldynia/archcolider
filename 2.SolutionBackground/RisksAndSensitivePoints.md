# Risks 

## Busniess related risks 

1. The catalog is stale and reserved food can't be dispatched from the selected smart-fridge. 
    - Option: Sync available items at purchase time to avoid reputational damages. 
2. Subscriber's menu can't be prepared. 
    - Options: Inform as soon as possible. Provide other meals from the same category. Add bonus coupons.  
3. Notification about delivery or meal can't be deliverd by prefered channel. 
    - Option 1: Delivery via backup communication channes.
    - Option 2: Do nothing if meal arrived to the point of dispatching.
    - Option 3: If meal didn't arrived, then create dedicated offer through PoS.
4. PoS app disconected from network. 
    - Option 1: Eventual consistency of operations. Send data when the network will be available. 
    - Option 2: Pin codes to grab a meal from Subscriber
5. Smart fridge disconected from network. 
    - Option 1: Generate pin code for dispatching as soon as possible so the fridge and user's app will have it upfront. Possibly a few days upfront.  
6. User booked a meal, but not picked up. 
    - Option: prepay to accomplish the operation.
7. Meal is stuck in the fridge. 
    - Options: User take a photo and file a complaint.

## Techical Risks 

1. Payment provider's service is temporarly down.
    - Options: All order records stored and requests to payment system can be retried for a defined period of time. Trust policy for known users and subscribers. 
2. Spawining too many service instances lead to money wastes. 
    - Option 1: Configured maximum possible number of instances for each service
    - Option 2: Safety threshold for instance spawning, then confirmaton from system administrator. 
3. Ghost Kitchen is down and do not provide information about meals availability
    - Option 1: Business as usual using the _ordering system_ internal information. In case of dispatching fail use compensation protocol. 
4. Not applying security practices. 
    - Option: Involve 3rd party white hat hackers to scan for vulnarabilities. 
5. Risky releases with big changes. 
    - Option 1: Enable hot swap for previous releases. Set requirement for platform provider. 
6. Breaking changes in message formats for internal or external services.  
    - Option 1: Back and forward compatibility serialization formats of messages. 
    - Option 2: Keep at least 1 backward compatibility conversion mechanism. API versioning.
    - Option 3: Early negotiation with "sunset" header attribute and alerts for such header.
7. Mismatch of production and development environment
    - Option 1: Negotiation of 1:1 problem. I.e. run in dev the same set of infrastructure elements: at least 1 item for purely infrastructure related services (proxies, firewalls, load balancers) and at least 2 instances for business related services (even if in prod there is only one). It help to identify many issues early.  

# Sensitive points 

## Business related 

1. Suscribers and Known users makes overprovisioning situation for a fridge. Not all food can be placed to a fridge. 
    - Option: _Need decision form the business how to handle this situation_. 
2. Order was placed during off hours of Ghost Kitchen. 
3. Revew bombing for a 3rd party kitchens.
    - Option: Review for service or meals available only for confirmed purchases. 

## Technical 

1. Modern cloud scaling technologies allows scaling up for a long time that might postpond decisions about scaling out. 
    - Business critical path scenario evaluation on production 
2. Service overloading
    - Proactive monitoring
    - Curcit breaker 
    - Dog Pile protection 
 
    


