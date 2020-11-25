# Deployment View 

The Deployment view focuses on aspects of the system that are important after the system has been tested and is ready to go into live operation. This view defines the physical environment in which the system is intended to run, including the hardware environment your system needs (e.g., processing nodes, network interconnections, and disk storage facilities), the technical environment requirements for each node (or node type) in the system, and the mapping of your software elements to the runtime environment that will execute them

The main concerns are: Types of hardware required, specification and quantity of hardware required, third-party software requirements, technology compatibility, network requirements, network capacity required, and physical constraints


## Components 


## Risks 


## Cost analysis


## Checklist 

* Have you mapped all of the system’s functional elements to a type of hardware device? Have you mapped them to specific hardware devices if appropriate?
* Is the role of each hardware element in the system fully understood? Is the specified hardware suitable for the role?
* Have you established detailed specifications for the system’s hardware devices? Do you know exactly how many of each device are required?
* Have you identified all required third-party software and documented all the dependencies between system elements and third-party software?
* Is the network topology required by the system understood and documented?
* Have you estimated and validated the required network capacity? Can the proposed network topology be built to support this capacity?
* Have network specialists validated that the required network can be built?
* Have you performed compatibility testing when evaluating your architectural options to ensure that the elements of the proposed deployment environment can be combined as desired?
* Have you used enough prototypes, benchmarks, and other practical tests when evaluating your architectural options to validate the critical aspects of the proposed deployment environment?
* Can you create a realistic test environment that is representative of the proposed deployment environment?
* Are you confident that the deployment environment will work as designed? Have you obtained external review to validate this opinion?
* Are the assessors satisfied that the deployment environment meets their requirements in terms of standards, risks, and costs?
* Have you checked that the physical constraints (such as floor space, power, cooling, and so on) implied by your required deployment environment can be met?
