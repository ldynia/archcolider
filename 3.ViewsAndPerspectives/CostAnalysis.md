# Cost analysis considerations

https://onedrive.live.com/edit.aspx?resid=91D2A6BED92B69C5!1028185&ithint=file%2cxlsx&authkey=!AOp6NCWeSf64J58

## Introduction
While selecting infrastructure and third party systems, we were governed preliminary by costs of the solution and limited budget of the client. In rare cases we decided to pick more expensive solutions the reason for that was convenience of chosen service to exceed its monetary value.

## Caveat Emptor
Provided costs are estimated base on the list of assumption mentioned below and projection of user growth and traffic they might generate.
Assumptions:
- We estimate that Farmacy Food will reach 100.000 users

## Projections
### Database size
Below image illustrates few tables/documents that might be used in the solution -it's of course simplified model. Nevertheless, we can see that generating **100K** record per month will take around **13.2 GiB** of storage space.

![database forecast](https://github.com/ldynia/archcolider/blob/master/3.ViewsAndPerspectives/docs/database_forecast.png)

### Data transferr size (traffic)
Traffic forecast was calculated base on the most frequent requests to the application API. Because, Farmacy Food users will have the ability to write feedback and reviews we will provide them the ability to uploading images. We assume that image size will take 4 MiB. Furthermore, we expect that monthly only 10% of the users writes reviews and 5% of users have some problems that leads to sending a feedback. As we can see that for **10K** requests per day (3 millions per month) we'll end up transferring to our application around **165 GiB** of data, and storing around **163 GiB** of images per month.  

![database forecast](https://github.com/ldynia/archcolider/blob/master/3.ViewsAndPerspectives/docs/traffic_forecst.png)

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
| API Gateway |AWS | Incoming requests |
| CloudFormation| AWS | Infrastructure as code solution |


## Cost

* [DataDog](https://www.datadoghq.com/pricing/) $15 USD

## Estimated cost bandwith

### Summary

|Service| 1-year TCO at minimum | 1-year TCO at projected growth | 1-year TCO at rapid growth |
| ----- | --------------------- | ------------------------------ | -------------------------- |
| EC2   | | | |
| AMAZON MQ | | | |
| Application Load Balancer | | | |
|DataDog| | | |

## Scaling scenarios


