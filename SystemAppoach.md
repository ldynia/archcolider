# System approach 

_Style, principles, patterns, design decisions_

## Principles

1. Messages over direct calls 
2. Telemetry is mandatory 
3. Exstensibility and modifability is top priority
4. Strive for cognitive simplicity

## Style

Based on provided principles the system should be n-tier with layered approach within modules that secure extensibility of functionality. We see it as a set of micro-kernels for each subdomain that communicates with messages (commands and events). Based on current [business goals](https://github.com/ldynia/archcolider/blob/master/Business%20goal%20and%20scope.md) (number of users, functionality current and desired) and [constraints](https://github.com/ldynia/archcolider/blob/master/Constraints.md) the major implementation style of architecute is monolitic start, but with an accent to hight modularity to lower cost of further extractions to independent services. 

All part subdomaing should provide rich telemetry of usage to make informative decision about extraction and next scaling if componnent become a bottleneck for the solution.  

