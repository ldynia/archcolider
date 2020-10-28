# Risks 

1. The catalog is stale and reserved food can't be delivered 
2. Subscriber's menu can't be prepared. 
3. Notification about delivery or meal can't be deliverd by prefered channel. 
4. PoS app disconected from network. 
5. Smart fridge disconected from network. 


# Sensitive points 

1. Suscribers and Known users makes overprovisioning situation for a fridge. Not all food can be placed to a fridge. 
2. Order was placed during off hours of Ghost Kitchen. 
3. Revew bombing for a 3rd party kitchens.

# Trade-offs 

1. The meals catalog sacrifice accuracy for availability at the time of browsing. It might mean that the catalog cached on the user's device and get updates ocassionally as it comes from upstream services. Also, we actually can't guarantee accuracy as we get info about in-stock items from the _smart-fridges system_ by API and we depends on fridges availability and connectivity. 


