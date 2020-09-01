---
layout: default
title: How to verify a Json Web Token with ORGiD ?
permalink: /docs/jwt/verify/
parent: Authentication
---

# How to verify a Json Web Token with ORGiD ?

To verify a JWT token, the sequence described in the [JWT Creation](/docs/jwt/create) are reversed:

1. Parse the JWT using standard libraries
    + Libraries should validate standard JWT fields like `exp` and `iat`
2. Using the `iss` field of the token, retrieve the associated JSON document using the process described in [ORGiD Discover](/docs/orgid/orgid-discover)
3. Validate the JWT signature using the Public Key provided in the document
4. Using the organization's JSON document, you can build your own validation logic prior to accepting a request:
    + Check that the requesting organization is not from a country under embargo in your own country
    + Check that the requesting organization is not a competitor
    + Enforce API rate limits and fair look-to-book ratios to avoid leaking business information
