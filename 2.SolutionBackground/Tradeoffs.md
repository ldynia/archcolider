# Trade-offs

1. The meals catalog sacrifices accuracy for availability at the time of browsing. Actual meal availability checks can happen during the payment initiation process. Users get used to that payment take some time, so the additional delay won't affect subjective performance perception.   
    - In practice, it means that the menu catalog caches on the user's device and get updates occasionally as it comes from upstream services. Also, we actually can't guarantee accuracy as we get info about in-stock items from the _smart-fridges system_ by API, and we depend on fridge availability and connectivity.
    - The second aspect of this trade-off is that we can also cache the response from the _smart-fridges system_ on the backend. There is a pretty high level of confidence in cache correctness as all the lion share of orders (in future perspective) will be processed by the _ordering system_ and keeping the cache in the actual state won't be so hard.
    - By this decision, we decrease pressure on the _smart-fridges system_ API, as we can request updates at a lower frequency unless fridges management doesn't provide subscriptions for updates.   
    
2. Event sourcing for order management with full history for data integrity and ease of incident investigation over relative/document storage. In this case, we trade simplicity and storage space for history and operations visibility. [ADR 009](../4.ADRs/007%20Event%20sourcing%20usage.md)
    - Event sourcing requires a deeper understanding of system behavior and accurate modeling of events that happen in the system. But in our case, we can treat it as a benefit for developers and BAs to model domain consciously.  
    - Event sourcing requires additional tooling support that might be developed in-house but better to use available commercial solutions to save time and increase the time-to-market rate.
     
3. In many cases, we are going to trade-off performance on the backend for data integrity. We want to secure accuracy in handling orders to keep users' satisfaction on a high level from our services. [ADR 008](../4.ADRs/008%20At%20least%20once%20delivery%20for%20ready%20to%20pay%20order.md)

4. Before the greater expansion of the system to other countries, it's better to use a payment provider service rather than implement the communication with Visa/MasterCard/AmEx/JCB/Paypal and so on. In this case, we save time and use a single API from the payment provider. Later it can be changed, as there is still an internal payment service on our side that can migrate handling communication with global payment systems step by step when necessary.
