# Authentication and Authorization

## Authentication
![Figure 1: High level overview of the authentication flow](/img/Authentication.png)
Figure 1: High level overview of the authentication flow

Figure 1 shows the general flow of authentication for customer/client access over the internet. This flow is **not** used for direct communication to AWS resources.

## Cognito
AWS offers a service called Cognito which we use here to handle our authentication needs. The flow described here is known as the [Authorization Code Grant](https://aws.amazon.com/blogs/mobile/understanding-amazon-cognito-user-pool-oauth-2-0-grants/).

> Some clients don't support redirect handling (302 handling) natively or by default. This is a common cause of error/misunderstandings in development.

Cognito has all the necessary forms built-in to use in your login, logout, profile etc. screens. Styling can be applied to brand all screens.

### Settings
- Make sure to use the User Pool setting in Cognito!
- Allow _with username_ for login
- Allow _verified e-mail address_ for login
- Add attributes to the identity data: phone number, email.
- Allow _openid_ scope
- Set the loadbalancer's _scheme_ to _internet facing_

## Federation

Federation allow for other authentication providers to be hooked up to our systems. A practical example of this is giving the user the option to login to *your system* using their google, facebook or other social media site login. The use of federation will immediately generate trust in your system with a large portion of potential users.

> Support non-federated authentication too. Some people may either trust *your* site less than the federated authentication provider's (ie. Google). This may make them sceptical. To futher support the availability of your own authentication provider, you should consider that users may want to use different passwords for different online service from a security perspective. 

## Loadbalancer

The design offered here uses the loadbalancer directly to provide authentication. The Https Listener is used with a set of rules that provide an action for checking the identity of the user requesting the resource. Once this is done we use the loadbalancers' rule to forward the traffic to the appropriate scaling group. (Also see: [Infrastructure Scaling and Balancing](/InfrastructureScalingAndBalancing.md)

## Pricing

Though the pricing of Cognito can be found on the pricing list on the AWS website, we would like to clarify one thing. The pricing of cognito is based on unique users per month. Billing **does not** go up if a user logs in multiple times per month nor when they perform multiple requests. If a user doesn't log in or register during a month you will not be billed for that user. Please check [AWS Cognito pricing](https://aws.amazon.com/cognito/pricing/) for up-to-date information.


