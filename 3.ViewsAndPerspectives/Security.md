# Security perspective 

The security perspective guides you as you consider the set of processes and technologies that allow the owners of resources in the system to reliably control who can perform what actions on particular resources.

The ability of the system to reliably control, monitor, and audit who can perform what actions on these resources and the ability to detect and recover from failures in security mechanisms

## Applicability to Views  
|  View | Aspects of applicability |
|------|---------|
| Functional | Reveals which functional elements need to be protected. Functional structure may be impacted by the need to implement your security policies. |
| Information | Reveals what data needs to be protected. Information models are often modified as a result of security design (e.g., partitioning information by sensitivity). |
| Concurrency | Security design may indicate the need to isolate different pieces of the system into different runtime elements, so affecting the system’s concurrency structure. |
| Development | Captures security related development guidelines and constraints. |
| Deployment | May need major changes to accommodate security-oriented hardware or software, or to address security risks. |
| Operational | Needs to make the security assumptions and responsibilities clear, so that these aspects of the security implementation can be reflected in operational processes. |

## Risks 



## Checklist for Architecture Definition and furter work 
- Have you addressed each threat identified in the threat model to the extent required?
- Have you used as much third-party security technology as possible?
- Have you produced an integrated overall design for the security solution?
- Have you considered all standard security principles when designing the infrastructure?
- Is your security infrastructure as simple as possible?
- Have you defined how to identify and recover from security breaches?
- Have you applied the results of the Security perspective to all of the affected views?
- Have external experts reviewed your security design?
