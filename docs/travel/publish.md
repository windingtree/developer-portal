---
layout: default
title: How to publish travel content on the marketplace?
permalink: /docs/travel/publish/
parent: Travel Content
---

# How to publish travel content on the marketplace?

This section describes how to publish travel content on the marketplace.

Travel content can be published directly by travel suppliers, by technology providers on behalf of suppliers, by travel content aggregators or by travel agencies.

Prequisites:

* [Register your organization](/docs/orgid/register/) in Winding Tree marketplace
* [Register your banking details](/docs/payment/account/) in Simard to receive payouts

## Accomodation providers

### Flow Overview

{% uml %}
participant "Travel Buyer" as B
participant "Marketplace" as M
participant "Simard Pay" as S
participant "Accomodation Provider" as H

note over B, H: Discovery
B->M: Retrieve Accomodation Providers and service APIs
activate M
M-->B:
deactivate M

note over B, H: Get Offers
B->H: POST /offers/search
activate H
H->H: Retrieve Availability, Rate and Inventory
H-->B: Offers
deactivate H
B->B: Select an offer

note over B, H: Book Offer
B->S: POST /balances/guarantees
activate S
S->S: Create Guarantee
S-->B: guaranteeId
deactivate S

B->H: POST /orders/createWithOffer
activate H
H->S: GET /balances/guarantees/{guaranteeID}
activate S
S-->H: Guarantee
deactivate S
H->H: Create Reservation
H->S: POST /balances/guarantees/{guaranteeID}/claim
activate S
S->S: Settle
S-->H: settlementId
H-->B: Order Details
deactivate H

{% enduml %}

### Creating Offers
#### Offer Request

For the details of the offer creation to comply with, see the [Open API schema](https://staging.b2b.glider.travel/api/docs/#/offers/offersWithSearchCriteria)

A search request from providers contains two main sections:

* `accomodation`: The details of the accomodation criteria
* `passengers`: The details of the guests

An `accomodation` object is composed of the following keys:

* `location`: Contains a GPS coordinate rectangle, circle or polygon.
* `arrival`: The desired check-in date and time
* `departure`: The desired check-out date and time

A `passengers` object is an array of passenger, which contains:

* `type`: The type of passengers (example: ADT, CHD)
* `count`: The passenger count for this passenger types

It is also possible to provide the passenger details directly from the search if the details are known at this stage, and the accomodation provider can use them to provide personalized offers.

{% uml %}
start

:Retrieve Buyer ORGiD Details;
if (Buyer accepted?) then (Yes)
  : Retrieve accommodations details;
  if (Accomnodations exist in the requested area?) then (Yes)
    :Retrieve availability, rates and inventory for each accommodation;
    if (Availability?) then (Yes)
      : Create offers and store in cache;
      : Return offers;
    else (No)
      : Return accommodation details;
    endif
  else (No)
    :Return 404 error;
  endif
else (No)
  :Return HTTP error;
endif
stop
{% enduml %}
