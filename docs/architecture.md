---
layout: default
title: Architecture
permalink: /docs/architecture/
nav_order: 2
---

# Architecture

## Overview

[Winding Tree](https://windingtree.com/) is a decentralized marketplace for travel businesses. As such, Winding Tree helps participants discover each other and transact automatically without intermediaries.

![Architecture Overview](/assets/images/architecture-overview.png)

## Protocol Stack

Winding Tree uses common standards and open protocols used in other industries. This allows to build fast and re-use libraries existing in most programming languages.

| Function       | Technology           |
| :------------- | :------------------- |
| Networking     | HTTP over TLS/TCP/IP |
| Authentication | [JSON Web Tokens](https://tools.ietf.org/html/rfc7519), powered by [ORGiD](https://docs.orgid.tech/) |
| Data Presentation | REST/JSON [OpenAPI](https://www.openapis.org/) with standadized schemas |

## Networking

To interact with an organization, you will need to gather the connection details.
The HTTP endpoint for the services is retrieve from the `service` section of the organization's JSON file.

The below is the `service` section for Glider Connect in test environment:

```json
[
  {
    "id": "did:orgid:0x94bf5a57b850a35b4d1d7b59f663ce3a8a76fd9928ef2067cc772fc97fb0ad75#apiv1",
    "serviceEndpoint": "https://staging.b2b.glider.travel/api/v1",
    "type": "glider",
    "version": "1",
    "description": "Glider Aggregator Ropsten Search and Book API",
    "docs": "https://staging.b2b.glider.travel/api/docs/"
  }
]
```

## Authentication

The authentication used in Winding Tree is the OAuth 2.0 Bearer Tokens, as described in RFC6750.

The tokens are following the JSON Web Tokens (JWT) standard.

It allows using very standard tools and libraries, for example using CURL:

```shell
curl -X GET "<service endpoint and path>" \
  -H  "accept: application/json" \
  -H  "authorization: Bearer <JWT Token>"
```

Using Postman:
![Postman Authorization preview](/assets/images/postman-authorization.png)

For guidelines on how to use JWT Tokens, see these dedicated section:

* [How to create a JWT Token?](/docs/jwt/create/)
* [How to verify a JWT Token?](/docs/jwt/verify/)

## Data Presentation

The API format is a REST/JSON with the data format enforced using OpenAPI 3.0.
The schemas are available below:

* [Search and Book API for travel content](https://staging.b2b.glider.travel/api/docs/)
* [Payment Accounts and Guarantees](https://staging.api.simard.io/api/docs/)

If you would like to propose schema changes or new schemas for other travel verticals, please open a Issue or Pull request on Github or get in touch!
