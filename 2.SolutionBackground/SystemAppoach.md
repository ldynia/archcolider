# System approach 

## Design Desicions 

### Service-based approach 

![](https://github.com/ldynia/archcolider/blob/master/img/FF_Overview_v1.PNG)

### Modularized services 

![](../img/FF_Modularization.PNG)

![](../img/FF_ModularizationExtraction.PNG)

### Event sourcing 

![](https://github.com/ldynia/archcolider/blob/master/img/FF_OrdersAndScheduler.PNG)

### Log-based communication for information propagation between services 

![](https://github.com/ldynia/archcolider/blob/master/img/FF_LogBasedStream.PNG)

### Health checks based on business critical path scenarious 

### Independent data storage for reporting 

## Alternatives 

Number of alternatives that was rejected for now. 

### Microservices from the start 

Microservice approach requires a lot of attention to infrastructure, separation of responsibility, preferably stable and known domain model. For the _ordering system_ it's not applicable and developers effort will be wasted for invisible for end users things. 

Microservices should grows naturally as need arise.

### Monolith 

This approach good for Prove of Concept approach and early stages of startup. Here we can see certain level of maturity, so pure monolith would be oversimplification.

## Composition of components 



## COTS 

### Event Store 

### Kafka 

### RabbitMQ 

### DataDog 







