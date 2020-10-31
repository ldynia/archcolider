# System approach 

_Style, principles, patterns, design decisions_

## Principles

1. Strive for cognitive simplicity 
2. Exstensibility and modifability prefered in case of trade-offs  
3. Telemetry is mandatory
4. Messages over direct calls

## Style

Based on provided principles the system should be n-tier with layered approach within modules that secure extensibility of functionality. We can imagin it as a set of micro-kernels for each subdomain that communicates by messages (commands and events). Based on current [business goals](https://github.com/ldynia/archcolider/blob/master/Business%20goal%20and%20scope.md) (number of users, functionality current and desired) and [constraints](https://github.com/ldynia/archcolider/blob/master/Constraints.md) the major implementation style of architecute is **modulaized monolith**, with an accent to hight modularity to lower cost of further extractions to independent services. 

According to declared principles we propose build system based on event sourcing and with domain driven design for core components. 
- Event sourcing helps to trace and reasoning about changes in domain models. It's necessary because many externals users involved and the system should provide detail investigation of every possible complaints from users about decision making, payment process and overall awareness. 
- Domain Driven Design (DDD) helps to control cognitive complexity of the subject area where necessary. Even if starting implementation requires more effort than transaction script approach or table based, it will save a lot of time in future. DDD also support declared principles of congnitive simplicity and modifability of the designed system.  

All part subdomaing should provide rich telemetry of usage to make informative decision about extraction and next scaling if componnent become a bottleneck for the solution. 

## Strategic domain design 

![Strategic Domain Design](https://github.com/ldynia/archcolider/blob/master/img/FF%20System%20-%20Strategic%20Domain%20Design.jpg)

