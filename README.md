# Architectural Katas 2020 Fall - Group ArchColider

### Resources

- [Architectural Katas](https://learning.oreilly.com/live-training/courses/architectural-katas/0636920458463/)
- [software-architecture-fundamentals](https://learning.oreilly.com/videos/software-architecture-fundamentals/9781491998991?autoplay=false)
- [fundamentals-of-software](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)
- [miro](https://miro.com/app/board/o9J_kh8andQ=/) - our diagrams
- [docs](https://docs.google.com/document/d/1SML3n4JbpZV2PSLRpjaCvBvyUMVsFwlqAQF3VKd_oPU/edit)

# Solution Structure

Table of content: 
- [Glossary](Glossary.md)
- [Questions to System Owner](Questions.md)
- [Problem Background](1.ProblemBackground/Readme.md)
	- [System overview](1.ProblemBackground/BusinessGoalAndScope.md)
	- [Goals and Context](1.ProblemBackground/FunctionalRequirements.md)
	- [Constraints](1.ProblemBackground/Constraints.md)
	- [Stakeholder](1.ProblemBackground/Stakeholders.md)
	- [Significant Driving Requirements](1.ProblemBackground/BusinessDrivers.md)
- [Solution Background](2.SolutionBackground/Readme.md)
	- [Solution Overview](2.SolutionBackground/SolutionOverview.md)
	- [Assumptions](2.SolutionBackground/Assumptions.md)
	- [Approach Summary](2.SolutionBackground/SystemAppoach.md)
	- [Tradeoffs](2.SolutionBackground/Tradeoffs.md)
	- [Risks and Sensitive points](2.SolutionBackground/RisksAndSensitivePoints.md)
	- [ADRs](4.ADRs/)
- [Views and Perspectives](3.ViewsAndPerspectives/Readme.md)
	- [User Scenarios](3.ViewsAndPerspectives/UserScenariosPerspective.md)
	- [Informational](3.ViewsAndPerspectives/InformationModels.md) 
	- [Concurrency](3.ViewsAndPerspectives/Concurrency.md)
	- [Deployment](3.ViewsAndPerspectives/DeploymentView.md)
	- [Cost Analysis](3.ViewsAndPerspectives/CostAnalysis.md) 
	- [Security](3.ViewsAndPerspectives/Security.md)

# ToDo 

Concerns to think about: 
- Throuput of the system in terms of business cases (avg, max). Use Lukasz's cases.
- Data storage estimation for all parts (back and front): now, in 6m, 1y and cost. Use Hemanth estimations. 
- Deployment scheme. Required services (Message Broker, Storage, Computatonal Instances, Log Streaming, balancers, etc), computational instances (? CPU, ? Memory). Get initial caps with prices and estimation for 1 year based on growth. In general Cost of Ownership. Mention later, that cost of development can't be estimated as selected language and market situation unknown for us. 
- Concurrency concerns. Identify weak points within the system, strategy for parallelism (scale horizontally and vertically) and when to apply. 

Pattrens to consider: 
- Backend for frontend (BFF)

To check again: 
- Auth models and capabilities 

Add: 
- ✅ Map providers integration https://developers.google.com/maps/solutions/store-locator 
- ✅ ADR: Stale data from fridges or kitchen 
- ✅ ADR: Client caching 
- ✅ Risk: SLA with 3rd party kitchens 
- [ ] Fitness functions\metrics for architecture 
- [ ] Failure and retry policies, identify recoverable and unrecoverable situations. How to handle them
- [ ] Donation concerns: senior citizens, low-income folks

Presentation plan: 
- requirements, what is odd there 
- scope and restrictions 
- conceptual mapping and applicability 
- quality attributes unique for different parts of the system, no common set 

Links: 
- Smart Fridge: https://bytetechnology.co/ https://thespoon.tech/byte-foods-opens-up-its-smart-vending-platform-with-byte-technology/
- Kiosk Point of Sale Software: https://pos.toasttab.com/
- Cheftec Kitchen Inventory Management Software: https://www.cheftec.com/cheftec-basic
- [chicken-truck-detroit-chef-phil-jones](https://eu.freep.com/story/entertainment/dining/mark-kurlyandchik/2020/06/11/chicken-truck-detroit-chef-phil-jones/5342730002/)
