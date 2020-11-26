# Cost analysis considerations

https://onedrive.live.com/edit.aspx?resid=91D2A6BED92B69C5!1028185&ithint=file%2cxlsx&authkey=!AOp6NCWeSf64J58

## Introduction
While selecting infrastructure and third party systems, we were governed preliminary by costs and limited burget of the client. In rare cases we decided to pick more expensive solutions becaouse convinience of given service exceed its monetary value.

## Caveat Emptor
At the time of writing we don't have a good indication of the traffic that should be handled by the infrastructure. However, this could end up causing a significant chunk of the total
cost of ownership (TCO) as the chosen cloud provider has data transfer costs. 

For now we handle this by:
- Making some assumptions about the loads that are to be expected.
- State a general cost indication that serves as a minimum.

## Infrastructure

That chosen AWS region is us-east due to the location being the closest to Detroit which is currently the largest market.

This part only shows infrastructure elements that have costs attached.

| (Cloud or SaaS) service | Provider  |Description |
| ------------- | --------  |------------- |
| EC2           | AWS       |Instance of a   |
| Amazon MQ     | AWS       | Managed service the can provide Rabbit MQ [ADR 4](/4.ADRs/004 Tracing and Monitoring Sytem.md)  |
| Application Load Balancer | AWS  | Load balancer for services running inside AWS. |
| Amazon Cognito | AWS  | Authentication and Authorization provider. |
| DataDog | DataDog | Metric and Event aggregator |
| SNS     | AWS | Notification Service used for push notifications |
| Cognito | AWS |  |
| Route 53 | AWS | Certificates (TLS) and DNS routing. |
| S3 Buckets| AWS | Storage services |
| CloudFormation| AWS | Infrastructure as code solution |


## Cost

## Estimated cost bandwith

### Summary

|Service| 1-year TCO at minimum | 1-year TCO at projected growth | 1-year TCO at rapid growth |
| ----- | --------------------- | ------------------------------ | -------------------------- |
| EC2   | | | |
| AMAZON MQ | | | |
| Application Load Balancer | | | |
|DataDog| | | |

## Scaling scenarios


