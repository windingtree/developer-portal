---
layout: default
title: Using GraphQL to explore the Marketplace
permalink: /docs/orgid/graphql/
parent: Marketplace
nav_order: 4
---

# Using GraphQL to explore the Marketplace

To facilitate the discovery and interaction with other organizations, Winding Tree provides a _Subgraph_ for GraphQL that indexes the content of the Winding Tree smartcontracts and the associated JSON documents.

The GraphQL node is published on The Graph for playground, however we recomend using your own infrastructure for a Production usage:

The Graph page with Playground:

* [Production (Mainnet) Subgraph](https://thegraph.com/explorer/subgraph/windingtree/orgid-subgraph)
* [Staging (Ropsten) Subgraph](https://thegraph.com/explorer/subgraph/windingtree/orgid-subgraph-ropsten)

GraphQL Endpoints:

* Production: `https://api.thegraph.com/subgraphs/name/windingtree/orgid-subgraph`
* Staging: `https://api.thegraph.com/subgraphs/name/windingtree/orgid-subgraph-ropsten`

This sections provides details on the GraphQL usage.

## GraphQL entity mapping

![GraphQL Entity mapping powered by Voyager](/assets/images/graphql-voyager.png)
[Zoom](/assets/images/graphql-voyager.png)

_Note_: Explore the GraphQL schema using [graphiql](https://graphiql-online.com) and using the above endpoints.

## Sample requests

### Get all directories

```graphql
{
  directories {
    segment
    isRemoved
    addedAtTimestamp
  }
}
```

```graphql
{
  "data": {
    "directories": [
      {
        "addedAtTimestamp": "1603753589",
        "isRemoved": false,
        "segment": "airlines"
      },
      {
        "addedAtTimestamp": "1603753613",
        "isRemoved": false,
        "segment": "ota"
      },
      {
        "addedAtTimestamp": "1603753593",
        "isRemoved": false,
        "segment": "insurance"
      },
      {
        "addedAtTimestamp": "1603753533",
        "isRemoved": false,
        "segment": "hotels"
      }
    ]
  }
}
```

### Retrieve the Public Keys of an Organization

```graphql
query($OrgId:ID = "0x4cbd3bfc50ec86b87b94f326a713b73d6b03c8e3531e9a891ddf68454a0b331a"){
  organization(id:$OrgId) {
    publicKey {
      did
      publicKeyPem
      type
    }
  }
}
```

```graphql
{
  "data": {
    "organization": {
      "publicKey": [
        {
          "did": "did:orgid:0x4cbd3bfc50ec86b87b94f326a713b73d6b03c8e3531e9a891ddf68454a0b331a#webserver",
          "publicKeyPem": "MFYwEAYHKoZIzj0CAQYFK4EEAAoDQgAEzFmGO9ULM9SKvyTX1I7gm3rs6XTTJRThRlNgRZSME1B6LPzAoElXwGdXI7e4kEhmF3UfM9dpkn9MGoQB72uD8g==",
          "type": "secp256k1"
        }
      ]
    }
  }
}
```

### Retrieve all Hotels in a specific area and their service APIs

```graphql
query($segment:String = "hotels"){
  directoryOrganizations(where:{
    segment:$segment,
    latitude_gt:"50.4",
    latitude_lt:"50.6",
    longitude_gt:"30.5",
    longitude_lt:"30.6",
  }) {
    organization {
      organizationalUnit {
        name
        address {
          gps {
            latitude
            longitude
          }
        }
      }
      service {
        serviceEndpoint
      }
    }
  }
}
```

```graphql
{
  "data": {
    "directoryOrganizations": [
      {
        "organization": {
          "organizationalUnit": {
            "address": {
              "gps": {
                "latitude": "50.44010749",
                "longitude": "30.5350227"
              }
            },
            "name": "Test Hotel"
          },
          "service": [
            {
              "serviceEndpoint": "https://api.myhotel.com/v1/"
            }
          ]
        }
      }
    ]
  }
}
```
