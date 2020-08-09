---
layout: page
title: Architecture
slug: architecture
---

### Overview
[Winding Tree](https://windingtree.com/) is a decentralized marketplace for travel businesses. As such, Winding Tree helps participants discover each other and transact automatically without intermediaries.

![Architecture Overview](/assets/images/architecture-overview.png)



### Protocol Stack

Winding Tree uses common standards and open protocols used in other industries. This allows to build fast and re-use libraries existing in most programming languages.

| Function       | Technology           |
| :------------- | :------------------- |
| Networking     | HTTP over TLS/TCP/IP |
| Authentication | [JSON Web Tokens](https://tools.ietf.org/html/rfc7519), powered by [ORGiD](https://docs.orgid.tech/) |
| Data Presentation | REST/JSON [OpenAPI](https://www.openapis.org/) with standadized schemas |

### Discovery

#### Registering an ORGiD
In order to be found on the marketplace, a participant should register on the marketplace and create its own ORGiD.

There are two ways to register an ORGiD:
* Using a web browser, Winding Tree hosts a user-friendly interface:
  * In live environment: https://marketplace.windingtree.com
  * In test environment: https://staging.arbor.fm
* Interacting with the Smart Contract directly: [guide](/doc/orgid-creation). This is relevant for travel businesses looking to register a large number of organizations (eg: Hotel Chains or Technology Providers).

#### Exploring ORGiDs
To find potential partners in the marketplace, one should browse the registered participants.

There are two ways to find other participants:
* Using a web browser, Winding Tree hosts a user-friendly interface:
  * In live environment: https://marketplace.windingtree.com/search
  * In test environment: https://staging.arbor.fm/search
* Interacting with the Smart Contract directly: [guide](/doc/orgid-discover). This is the recommended approach for developers.

