---
layout: default
title: How to register my organization?
permalink: /docs/orgid/register/
parent: Marketplace
nav_order: 3
---
# How to register an Organization?

## Initial Registration

In order to be found on the marketplace, a participant should register on the marketplace and create its own ORGiD.
To know more about ORGiD : https://blog.windingtree.com/everything-you-need-to-know-about-org-id-6c1c6172ae55
There are two ways to register an ORGiD:

* Using a web browser, Winding Tree hosts a user-friendly interface:
  * In live environment: [https://marketplace.windingtree.com](https://marketplace.windingtree.com)
  * In test environment: [https://staging.marketplace.windingtree.com](https://staging.marketplace.windingtree.com)
* Interacting with the Smart Contract directly. This is relevant for travel businesses looking to register a large number of organizations (eg: Hotel Chains or Technology Providers).
## Creating an ORGiD through Marketplace
You need to have an Ethereum wallet to sign in to the marketplace.If you don't have one already, you can create a wallet on the marketplace and then continue to register ORGiD. <img width="368" alt="image" src="https://user-images.githubusercontent.com/95684171/152492097-cb1eb355-0794-41f5-a768-45f500345a8b.png">

*Visit the marketplace website (live https://marketplace.windingtree.com/ or test env https://staging.marketplace.windingtree.com)
*Connect your Etherium wallet 
*Click on the Sign Up Button on the webpage and enter details of your Organization in the form.
*Once you save your Organization info, you'll need to pay a small registration fee<img width="934" alt="image" src="https://user-images.githubusercontent.com/95684171/152493247-622e8d6b-8599-4349-8ffc-732cc35d8d10.png">
*Once the fee is paid, yoir organization will become live on the Marketplace.You can then navigate to your Organization Profile and view the ORGiD created.<img width="950" alt="image" src="https://user-images.githubusercontent.com/95684171/152493798-92639574-a2d9-433a-b896-e07927042ea9.png">


## Creating an ORGiD programatically

### The two components of ORGiD

A Travel Business that wishes to participate directly on the Winding Tree ecosystem is represented by a set of two components:

* _An ORGiD Identifier_: This is a unique 64-bytes hexadecmial string identifier, similar to a registration number provided by a country's business registry. This identifier is normally created by the ORGiD smartcontract automatically, but it can be chosen if is not yet in used.
* _An associated JSON document_: This is a machine-readable file that contains all the details of the travel business. It is not stored on the blockchain for performance and costs reasons, but rather hosted by a traditional webserver.

The JSON document provides a structured representation of the travel business. It contains elements that can be found in a business registry, enriched with information that allows developers to interact with the business:

* Details of the legal entity, such as the legal name and address
* List of services exposed, such as availability and booking services and their format.
* Associated authentication public keys
* A set of assertions (or "proofs") allowing another party to validate that the contract is indeed associated to the travel business entity.

The ORGiD contract mainly references the JSON document, but it also provides mechanisms to update it and verify its integrity. The ORGiD content is fully owned by the travel business, the ownership being provided by the Ethereum blockchain.

### Preparing a JSON File

The JSON file representing the organization is an extension of the [W3C Decentralized Identifiers](https://w3c.github.io/did-core/), and must comply with the [ORGiD JSON Schema](https://github.com/windingtree/org.json-schema).

The above repository contains two [examples](https://github.com/windingtree/org.json-schema/tree/master/examples) of JSON document.

Make sure your file is valid as per the schema, otherwise other participants will not be able to discover or interact with your organization.

Once it is created, it can be stored in any place as long as it can be served over HTTP. Since it might be retrieved very often by other participants, it is important to store it in a place where the availability is ensure and that can handle a large amount of requests.

For example:

* Git repository
* [IPFS](https://ipfs.io)
* CDN / Cloud Hosting provider

The smartcontract allows to provide _three_ external links with your JSON file: one main location and two additional backup locations.

### Creating a Hash

Having the document stored outside the Ethereum chain, there is a risk that a third party could alter its content without the owner knowing it. To protect the integrity of the document, and allow third parties to verify the document has been created by the owner of the organization, a hash of the document is stored in the ORGiD smartcontract.

The expected hashing mechanism is `Keccak256`, this hash mechanism is widely used in Ethereum and standardized as SHA-3 by NIST. This hashing mechanism is built-in in the Ethereum ecosytem.

### Inserting your organization in the ORGiD smartcontract

Now that you have all elements, you can publish the organization in the ORGiD smartcontract.

The registration is made by calling the `createOrganization()` function from the [ORGiD smart contract](https://github.com/windingtree/org.id).
