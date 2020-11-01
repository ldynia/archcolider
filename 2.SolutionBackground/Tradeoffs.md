# Trade-offs 

1. The meals catalog sacrifice accuracy for availability at the time of browsing. Actual meal availability checks can happen during payment initiation process. Users get used that payment take some time so additional delay won't affect subjective perfomance perception.   
    - In practice it means that the menu catalog cached on the user's device and get updates ocassionally as it comes from upstream services. Also, we actually can't guarantee accuracy as we get info about in-stock items from the _smart-fridges system_ by API and we depends on fridges availability and connectivity. 
    - The second aspect of this trade-off that we can also cache response from the _smart-fridges system_ on the back-end. There is a pretty high level of confidence in cache correctness as all the lion share of orders (in future perspective) will be processed by the _ordering system_ and keep cache in actual state won't be so hard. 
    - By this decision we decrease preassure on the _smart-fridges system_ API, as we can request updates at lower frequence, unless fridges management doesn't provide subscription for updates.   
    
2. Event sourcing for order management with full history for data integrity and ease of incident investigation over relative/document storages. In this case we trade simplicity and storage space for history and operations visibility. [ADR 009](https://github.com/ldynia/archcolider/blob/master/4.ADRs/009%20Event%20sourcing%20usage.md)
    - Event sourcing requires deeper understanding about system behaviour and accurate modeling of events that happening in the system. But in our case we can treat it as benefit for developers and BAs to model domain consciously.  
    - Event sourcing requires additional toolng support that might be developed in-house but better to use available commercial solutions to save time and increase time-to-market rate. 
    
3. In many cases we going to trade-off performance on backend for data integrity. We'd like to secure accuracy in handling orders to keep user's satisfaction on high level from our services. 

4. Before greater expansion of the system to other contries it's better to use a payment provider service rather than implement communication with Visa/MasterCard/AmEx/JCB/Paypal and so on. In this case we save time and use a single API from payment provider. Later it can be changed, as there is still internal payment service on our side, that can migrate  handling communication with global payment systems step by step when necessary. 


