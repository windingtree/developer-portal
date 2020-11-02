---
layout: default
title: How to interact with the ORGiD smartcontract?
permalink: /docs/orgid/connect/
parent: Marketplace
nav_order: 1
---

# How to interact with the ORGiD smartcontract ?

Interacting directly with the ORGiD smartcontract let developers freedom to innovate with the Winding Tree marketplace.

Connecting to an Ethereum node is needed only for advanced usages, for simpler usage developers can rather connect to a GraphQL node, see [How to find other participants](docs/orgid-discover).

## Connect to an Ethereum node

In order to interact with the ORGiD smartcontract, you will need to connect to an Ethereum node.

There are multiple options to connect to an Ethereum node:

* Register with a cloud provider such as [Infura](https://infura.io/) or [Azure Blockchain Service](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.Blockchain?tab=Overview) to get started in minutes
* Buy specialized hardware, like [Dappnode](https://dappnode.io)
* Install and run your own instance of an Ethereum client such a [Geth](https://geth.ethereum.org/)

Once you have your node ready, you will get an HTTPS and/or Websocket endpoint that can be used to connect to the Ethereum network.

In the case of Infura, it looks like this:

* Production:
  * HTTP Endpoint: `https://mainnet.infura.io/v3/<project_id>`
  * Websocket: `wss://mainnet.infura.io/ws/v3/<project_id>`
* Test System (Ropsten):
  * HTTP Endpoint: `https://ropsten.infura.io/v3/<project_id>`
  * Websocket: `wss://ropsten.infura.io/ws/v3/<project_id>`

You can then connect using some libraries:

| Language | Libraries |
|:---------|:----------|
| Python | [Web3](https://web3py.readthedocs.io/) |
| Javascript / NodeJS | [Web3](https://web3js.readthedocs.io) or [Ethers](https://docs.ethers.io/v5/) |

## Retrieve the contract ABI

In order to interact with an Ethereum smartcontract, you will need the Application Binary Interface (ABI) of the ORGiD smartcontract.

The latest version can be retrieved from JSDeliver [ORGiD package](https://www.jsdelivr.com/package/npm/@windingtree/org.id), in the path `/build/contracts/OrgId.json`. Only the `abi` key in this JSON file is needed.

## Interact with the ORGiD smartcontract functions

Below are the most interesting functions of the ORGiD smartcontract:

| Function | Purpose |
|:---------|:--------|
| `createOrganization` | Creates a new organization in the marketplace |
| `createUnit` | Creates a new organization unit under a parent organization |
| `toggleActiveState` | Allows enabling or disabling an organization |
| `transferOrganizationOwnership` | Transfers organization ownership to new owner |
| `setOrgJson` | Sets a new JSON document URI, including a hash of the file to prevent tampering |
| `getOrganizations` | Get all active organizations |
| `getOrganization` | Get the details of a given organization |
| `getUnits` | Get all organization units belonging to an organization |

For the details of the parameters to be used, please refer to the [ORGiD Repository](https://github.com/windingtree/org.id)
