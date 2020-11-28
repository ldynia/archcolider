# Use of Infrastructure as Code (IaC)

Date: 2020-11-24

## Status

Draft

## Context

Infrastructure deployment, in the traditional imperative way, is prone to oversights and errors or beholden to extremely rigorous processes that stifle change. Hunting down a small deviation from the design, such as having accidentally added a public IP to a machine, can spell disaster. 

Perpendicular to imperative specifications there are declarative specifications of infrastructure. These declarative specifications describe the desired state in favour of the steps to reach such a state. Infrastructure as code is a way to script the declarative specification using a Domain Specific Language or a General Programming Language. 

## Decision

Infrastructure as Code allows us to prevent infrastructure drift and allows us to run architectural fitness functions on the specification instead of the run-time environment. This in turn allows us to test many scenarios without actually setting the deployment of the infrastructure in motion.
We are guaranteed to run the tests against what will in fact be deployed when we decide to execute the specification. Therefore, creating a very agile and evolvable ecosystem.
 
We can recommend **Cloudformation** because it has built-in AWS specific features that assist the infrastructure engineer using visual designers but also checks on valid configurations. However, this is not officially part of the ADR as we recognize that an alternative, such as Terraform, could already be mastered by the implementation team.

## Consequences

- The team will lose the ability to make ad-hoc changes without causing drift. Depending on the drift detection settings this may result in operational issues. Possibly even worse, you may assume the desired state while not being aware of the drift.

**Positive:**
- **Infrastructure code files can be checked into source control.**
- **Can be integrated into CI/CD**
- IaC can be used to promote DevOps.
- Repeatable due to idempotency
- Drift detection
- Remediation


**Negative:**
- IaC APIs can be daunting at first.
- IaC API documentation can be less mature than desired. **This depends on the provider of the resource you want to provision.**
- Manual tweaks to the infrastructure at run-time cause drift.

**Risks:**
- Incorrect policies set on the provisioning role (the role that executes the IaC) can result in escalated privileges on the run-time infrastructure environment. Even though this is not a problem specific to IaC it is, however, more prevalent.

**Bonus Features:** 
- Drift detection when manual changes are forced to the infrastructure. You could set up alerts for such a scenario so action can be taken. Furthermore, if you decide to use Cloudformation you could use RemediationConfiguration(s) to take a certain action that can go beyond a simple message. For instance, in the case of the example above (the public IP address being attached to an ENI )

- It is reasonably easy to use standard transformations to create derived environments (ie. Development, Test, Production, etc.). This may vary from rather crude XSTL file-based solutions to more sophisticated options.
