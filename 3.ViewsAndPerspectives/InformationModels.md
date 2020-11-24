# Information models 

## Cases 

### Case X 

#### Stakeholders concerns 

#### Diagrams 

#### Lifetime concerns 

### Case Y

#### Stakeholders concerns 

#### Diagrams 

#### Lifetime concerns 

## Estimations of usage and costs

## Backup concerns 

- We don't need to backup data for orders in MQ, as the client app should implement a timeout mechanism for sending requests and getting responses. If there is no confirmation about payment acceptance or rejection, a user should be notified and retry should be offered. So for MQ we can rely on the build-in persistence model for the service restart scenario.
- EventStore requires a backup mechanism as it vital information for the system. Projections do not require backup as they can be reconstructed from events in EventStore. But we can backup projections to speedup the recovery scenario.
- Report service requires backup mechanism.
- Kafka do not require and we can rely on a build-in mechanisms.




