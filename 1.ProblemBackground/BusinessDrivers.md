# Business Drivers (BD)

## Business goal:

*A “ghost kitchen” (food preparation and cooking facility set up for the preparation of delivery-only meals.) needs an ordering system to allow users to have visibility of what items are available, purchase, and pick up items at any one of their points of sale / smart-fridge.*

1. System support and engage occasional users to purchase to increase the user base, converting Occasional users to Known users and Known users to Subscribers.
2. System provides rich options for engaging known users and subscribers by different kinds of loyalty programs. New options are easily added to increase user satisfaction and a chance of recommendation.
3. System provides information about consumed meals and on-demand requests to support Ghost Kitchen management.
4. System should be easy to use for inexperienced users to increase the user base.
5. Sustainable usage of service.
6. Involve other specialists in health areas to increase userbase.

# Significant Architectural Requirements (SAR)

List of architecture driving requirements (primary functional, quality attribute, and life-cycle requirements)

| # | Significant Architectural Requirements | From BD |
|----|----|----|
| 1 | System support cash and electronic payments | 1 |
| 2 | Pluggable system of feedback, survey, review abilities | 1, 2 |
| 3 | On-time reports about consumed meals from fridges. Breakdown by subscribers and occasional buying | 3 |
| 4 | Scheduling system for subscribers, to avoid repetitive operations of ordering | 1, 3, 4, 5 |
| 5 | Ability to purchase without registering first | 1, 4, 5 |
| 6 | Notification system to inform the user about their orders | 1, 4, 5 |
| 7 | Notifications about new loyalty programs and coupons | 2, 5 |
| 8 | Detailed break down of a meal by components in catalog | 1, 5, 6 |
| 9 | Secure payments | 1, 5 |
| 10 | Maximizing guarantee of a meal picking up by user | 1, 5 |

# Detalization of SARs

## 1. System support cash and electronic payments.

1. Cash payments supported by _PoS Admin_ and dedicated application for _Occasional users_
2. Users can add different payment methods to the App.
3. New payment method is easy to add within a man/month for new areas.
4. User can spend virtual funds (coupons and discounts) for payments.

## 2. Feedback functionality - Pluggable system of feedback, survey, review abilities

1. System reminds the user to add a review for a meal if it wasn't done before.
2. Users can read reviews for any meal in the catalog.
3. User can easily provide feedback about any aspect of the service.
4. Reviews grouped and categorized for the Owner.
5. Support for in-App surveys.
6. Users can provide a review only for actually used services. I.e. review only for bought meals.
7. Ease of introducing engaging activities for the owner.

## 3. Reporting functionality

1. Ghost kitchen can browse and query the menu schedule of subscribers
2. Ghost kitchen receive a report about consumed meals with a possible breakdown by PoS, subscribers, occasional buying

## 4. Scheduling functionality

1. Subscriber can form a menu for a week, prepaid, and set a pickup time.
2. Subscriber can browse the created menu.
3. Subscriber can cancel the menu and get notification about it.
4. Subscriber can reorder the same menu for a previous time period in one click. (Possibly subscriber can select from any previous pre-formed menus)
5. Known user or subscriber can make an order and reserve time for picking up an order. It's treated as a scheduled order.

## 5. Purchase functionality

1. _PoS admin_ impersonate system user and make an order from the smart-fridge in the local PoS
- _PoS admin_ has a personal account and login. It's not a generic account for a PoS.
2. Any user can make a purchase and use any payment method supported by PoS
- In fact, it can be dismissed, as _PoS admin_ enter price value for "logging" purposes. So we don't care at all. (AG)
3. (crazy idea) Smart-fridges can have a QR code that will navigate to a web-page of a specific fridge, where the user can make an order or get info about meals. (not our case, because still pay through smart-fridge terminal and it out of scope and responsibility)
4. Purchase can be covered by coupons, bonus points and money (electronic and cash) in any proportion.

## 6. Notification functionality

1. Users get notification about any significant action related to actual ordering: payment process (initializing and result), availability of food for pickup, canceling, out of a stock situation.
2. User can set a preferred way of notification: in-app, push, SMS, email.
3. User get notification about significant changes in account state.

## 7. Loyalty functionality

1. Notification about non-ordering events should be managed separately.
2. Users can set preferred way of notification: in-app, push, SMS, email.
3. User has a dedicated account with accumulated coupons and bonuses.
4. User can split a payment and cover part of the order with coupons\vouchers\bonus points.  
5. User earn loyalty points for participating in feedback program, planned purchases, ad campaigns, and other activities suggested by system owner.  

## 8. Maximizing guarantee of a meal picking up by a user

1. Users can use a registered card(s) to authorize the pickup process.
2. Pre-generated codes for pickup allows impersonated meal collecting. (ADR 002)
