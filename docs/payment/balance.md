---
layout: default
title: How to register an account and access my balance?
permalink: /docs/payment/balance/
parent: Payments
nav_order: 2
---

# How to register an account and access my balance?

Simard Pay maintains the balance of participants on the Winding Tree marketplace. The balances are credited as soon as bank transfers are received, and funds can be withdrawn at any time by the participants.

The API is kept very simple to use as most details required by banking partners are automatically retrieved from the ORGiD profile.

{% uml %}
title Payment Mechanism Overview

participant "Travel Buyer" as B
participant Simard as S
participant "Travel Supplier" as T

B->S: POST /accounts with IBAN and currency
activate S
note left of S: Simard registers the IBAN and\nassociate it to the ORGiD
S-->B: Ack
deactivate S

T->S: POST /accounts with IBAN and currency
activate S
S-->T: Ack
deactivate S

B->S: GET /balances/depositInstructions
activate S
note left of S: Simard provides bank account details\nfor bank transfers in the supported currencies.
S-->B: Bank accounts details
deactivate S

B->S: [Financial] Bank Transfer
activate S
S->S: Update ORG.ID balance
note left of S: Simard is notified of incoming bank transfer\nand update the balance of the participants.
deactivate S

note over B,T: Participants transact on the platform\nBalance is modified with Guarantees and Claims

T->S: POST /balances/{currency}/withdraw
activate S
note right of S: When a participant wants to withdraw its balance\nSimard initiates a bank transfer for the payout.
S-->T: Ack
S->T: [Financial] Bank Transfer
deactivate S
{% enduml %}

Simard's bank is participating in the European SEPA Instant Credit scheme and in the UK Faster Payment Service, therefore bank transfers in supported currencies are credited can be settled in near real time, providing of course that the participant's bank is also part of such scheme.

Caveats:

* There is no currency exchange mechanism implemented yet, therefore buyers must ensure they have sufficient funds in the travel supplier's indicated currency before making a guarantee.
* There is no user interface yet to monitor the balances and deposits. However all information is available using Simard's APIs.
