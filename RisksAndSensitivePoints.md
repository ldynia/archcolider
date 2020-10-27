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

Risk #5. 
ADR: 
  Solution: Secruity codes generated and delivered upfront for a next day. 
  Conslusions: 
   - Code should long enought to avoid brute force. 
