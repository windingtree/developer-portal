---
layout: default
title: How to create a guarantee for another participant?
permalink: /docs/payment/guarantee-create/
parent: Payments
---

# How to create a guarantee for another participant?

Providing that a travel buyer has deposited funds on Simard, it can create a guarantee for a travel supplier. The below diagram describes this exchange.

{% uml %}
participant "Travel Buyer" as B
participant "Travel Supplier" as S
participant "Simard Pay" as Simard

B->S: Request Quote
activate S
S-->B: Quote
deactivate S

B->Simard: Create guarantee
activate Simard
Simard->Simard: Reserve funds
Simard-->B: guaranteeId
deactivate Simard

B->S: Create Order {guaranteeId}
activate S
S->Simard: Verify Guarantee
activate Simard
Simard-->S: Guarantee details
deactivate Simard
S->S: Deliver service
S->Simard: Claim guarantee
activate Simard
Simard->Simard: Settle funds
Simard->S:
deactivate Simard
S-->B: Order
deactivate S

{% enduml %}
