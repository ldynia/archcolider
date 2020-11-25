# Infrastructure Services and (virtual) hardware

![Figure 1: Services overview](/img/services.png)
Figure 1: Services overview

> **Note: ** The second subnet is a copy of subnet 1 when instanced from the Infrastructure as Code specification. Scaling can create more copies on-demand.

## Core server
The software architecture is classed as a modular monolith. (See: [ADR 003: System approach](/4.ADRs/003%20System%20approach.md)) In Figure 1 we have used a single core server as an example.
Of course, this doesn't accurately represent the actual scaling of the systems but it serves to focus you to on the important bits for the purpose of this discussion.

The core server represents a template of the server and the modules it contains.

## Amazon MQ (_MQ_)
As we have a modular monolith we should treat the modules as if they were not part of a single monolith. Modules are allowed to "talk" to each other by using a queue. We have decided on the use of Amazon MQ to provide us with such queue capabilities.

## Kafka Managed Streams (_Kafka_)[1](#footnotes)
Once again, we have chosen to use a AWS native service for our streaming needs. This component of the infastructure allows us communication that goes beyond intra-module communication. We use this for notification requests, metrics export and data reporting.

## Amazon Simple Notification Service (_SNS_)
SNS is a notification service that serves as a facade for multiple notification options. The use of this service will allow us to send SMS texts, e-mail or mobile push messages when certain events occur. Examples of such events are:
- Meal is available for pick-up
- Customer friendly messages for unexpected/undesirable conditions. (Meal out of stock, payment failed etc.)

## DataDog
_DataDog_ is a SaaS offering that lives outside of _AWS_. _DataDog_ is used to receive, analyze and report on metrics provided by our systems. _DataDog_ is to be used as an aggregator of all our metrics data. (Exceptions may apply)

## Tableau
Reporting on user generated data can be of vital importance to the company. _Tableau_ is a well-known player in the reporting market and trusted by many companies. _Tableau_ reports server as a way to identify crucial pivot points for your company.

## Point of Sale (PoS)
The _Point of Sale_ system, while being out of scope for this project, is an external system that we have to integrate with.

## Ghost Kitchen
See [Ghost Kitchen](/Glossary.md)

## Footnotes
1: We use Kafka as a abbreviation (of sorts) here because _KMS_ is already a term used in _AWS_ and we believe this might cause confusion.
