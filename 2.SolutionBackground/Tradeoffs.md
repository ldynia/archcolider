# Trade-offs 

1. The meals catalog sacrifice accuracy for availability at the time of browsing. Actual meal availability checks can happen during payment initiation process. Users get used that payment take some time so additional delay won't affect subjective perfomance perception.   
    - In practice it means that the menu catalog cached on the user's device and get updates ocassionally as it comes from upstream services. Also, we actually can't guarantee accuracy as we get info about in-stock items from the _smart-fridges system_ by API and we depends on fridges availability and connectivity. 
    - The second aspect of this trade-off that we can also cache response from the _smart-fridges system_ on the back-end. There is a pretty high level of confidence in cache correctness as all the lion share of orders (in future perspective) will be processed by the _ordering system_ and keep cache in actual state won't be so hard. 
    - By this decision we decrease preassure on the _smart-fridges system_ API, as we can request updates at lower frequence, unless fridges management doesn't provide subscription for updates.   
    

