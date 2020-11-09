---
layout: default
title: How to verify a Json Web Token with ORGiD ?
permalink: /docs/jwt/verify/
parent: Authentication
---

# How to verify a Json Web Token with ORGiD ?

## Overview

To verify a JWT token, the sequence described in the [JWT Creation](/docs/jwt/create) are reversed:

1. Parse the JWT using standard libraries
    + Libraries should validate standard JWT fields like `exp` and `iat`
2. Using the `iss` field of the token, retrieve the associated JSON document using the process described in [ORGiD Discover](/docs/orgid/orgid-discover)
3. Validate the JWT signature using the Public Key provided in the document
4. Using the organization's JSON document, you can build your own validation logic prior to accepting a request:
    + Check that the requesting organization is not from a country under embargo in your own country
    + Check that the requesting organization is not a competitor
    + Enforce API rate limits and fair look-to-book ratios to avoid leaking business information

Note that the Public Keys of an organization can be retrieved using the GraphQL node in a single call.

## Code Examples

### Using Python

```python
import re
import requests
import yaml
import jsonschema

# Let's assume the recipient is Glider
recipient = 'did:orgid:my_recipient_orgid'
jwt_token = 'eyJ0eXAi...' 
now = int(datetime.utcnow().timestamp())

# Decode the token with signature verification disabled as we do not have the Public Key yet
claims = jwt.decode(jwt_token, verify=False)

# Check for mandatory claims
assert(claims['aud'] == recipient)
assert(claims['exp'] > now)

# Check for the optional claims
if 'nbf' in claims:
    assert(claims['nbf'] < now)
if 'iat' in claims:
    assert(claims['iat'] < now)

# Parse the iss claim
m = re.match(r'^did:orgid:(?P<orgid>0x[A-Za-z0-9]{64})#(?P<fragment>.+)$', claims['iss'])
assert(m != None)
sender_orgid = m.group('orgid')

# Retrieve and validate the Organization details from the contract
result = orgid_contract.functions.getOrganization(bytes.fromhex(sender_orgid[2:])).call()
sender_organization = Organization._make(result)
assert(sender_organization.exists)
assert(sender_organization.state)

# Retrieve the JSON Document
doc = requests.get(sender_organization.json_uri)
assert(w3.sha3(text=doc.text) == sender_organization.json_hash)

# Validate the JSON Structure
orgid_schema = requests.get('https://raw.githubusercontent.com/windingtree/org.json-schema/master/src/orgid-json-schema.yaml').text
yaml_validator = yaml.load(orgid_schema, Loader=yaml.FullLoader)
jsonschema.validate(doc.json(), yaml_validator)
                    
# Retrieve the Public Key
found = False
for publicKey in doc.json()['publicKey']:
    if publicKey['id'] == claims['iss']:
        found = True
        break
assert(found)        

# Validate the JWT signature
d = jwt.decode(jwt_token, publicKey['publicKeyPem'], audience=recipient)

# The application can then safely interact with the organization
# For example using the company legal information
print(doc.json()['legalEntity'])
```

### Using Javascript

```javascript
const { JWK, JWT } = require('jose');
const { OrgIdResolver, httpFetchMethod } = require('@windingtree/org.id-resolver');
const { addresses: orgIdAddresses } = require('@windingtree/org.id');
const { addresses: lifDepositAddresses } = require('@windingtree/org.id-lif-deposit');

// ORG.ID resolver configuration
const defaultNetwork = 'mainnet'; // or ropsten for test
const orgIdResolver = new OrgIdResolver({
    web3, // Web3 client initialized
    orgId: orgIdAddresses[defaultNetwork],
    lifDeposit: lifDepositAddresses[defaultNetwork]
});
orgIdResolver.registerFetchMethod(httpFetchMethod);

const verifyJWT = async (jwt) => {
  
    // Decode the token using JWT library
    const decodedToken = JWT.decode(jwt, {
        complete: true
    });
    const { payload: { exp, aud, iss } } = decodedToken;

    // Issuer should be defined
    if (!iss || iss === '') {
        throw('JWT is missing issuing ORG.ID');
    }

    // Resolve did to didDocument
    const { did, fragment } = iss.match(/(?<did>did:orgid:0x\w{64})(?:#{1})?(?<fragment>\w+)?/).groups;

    const didResult = await orgIdResolver.resolve(did);

    // Organization should not be disabled
    if (!didResult.organization.isActive) {
        throw(`Organization: ${didResult.organization.orgId} is disabled`);
    }
    
    // Retrieve the Public Key PEM
    const publicKey = didResult.didDocument.publicKey.filter(
        p => p.id.match(RegExp(`#${fragment}$`, 'g'))
    )[0];

    if (!publicKey) {
        throw('Public key definition not found in the DID document');
    }

    if (!publicKey.publicKeyPem.match(RegExp('PUBLIC KEY', 'gi'))) {
        publicKey.publicKeyPem = `-----BEGIN PUBLIC KEY-----\n${publicKey.publicKeyPem}\n-----END PUBLIC KEY-----`;
    }

    // Load Public Key as a JWK
    const pubKey = JWK.asKey(
        publicKey.publicKeyPem,
        {
        alg: 'ES256K',
        use: 'sig'
        }
    );

    // Throws if the verification fails
    JWT.verify(
        jwt,
        pubKey,
        {
            typ: 'JWT',
            aud: 'replaceWithYourDid'
        }
    );

    return {
        aud,
        iss,
        exp,
        didResult
    };
};
```
