# Assumptions

## Smart fridges

1. We assume that there are methods that allow us to know about the current stock, dispatching, time of refillment, and so on. 
2. Stock refillment happens one-two times per day at a roughly predictable time. It happens because of the physical ability to deliver meals based on demand, traffic situation, ghost kitchen payloads. 

## Ghost Kitchen 

1. Ghost kitchen can provide feedback about order executing, like: accepted, dispatched, can't do, delayed
2. Ghost kitchen do not work 24/7 and prepare orders received at the beginning of the working day. 
3. Ghost kitchen already uses some tracking system that has some form of API that accepts writes.
4. [Inventory](../Glossary.md) updates are not limited by changes in the stock of smart-fridges for a refill.
5. Inventory updates can be formed by the user's request for the desired meal. A User can be a Subscriber or a Known user.
6. Inventory updates created by scheduling system from subscribers menu for a week/month.

## Development team

1. Development team is relatively small, and the proposed solution should enable fast time-to-market and ease of changes 
2. Development team is cross-functional and have experience with major technologies available on the market
