---
layout: default
title: How to interact with the ORGiD smartcontract?
permalink: /docs/orgid/connect/
parent: Marketplace
nav_order: 1
---

# How to interact with the ORGiD smartcontract?

Interacting directly with the ORGiD smartcontract let you do everything you want with the Winding Tree marketplace.

## Connect to an Ethereum node

In order to interact with the ORGiD smartcontract, you will need to connect to an Ethereum node.

There are multiple options to connect to an Ethereum node, for starters we recomend using an hosted node service such as [Infura](https://infura.io/) instead of running your own Ethereum node. You can decide to use another Ethereum hosted node, or host your own node, this is completly at your discretion.

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

Here is the ABI for version 1.0.1 of the ORGiD smarcontract:

```json
[{
    "anonymous": false,
    "inputs": [
    {
        "indexed": true,
        "internalType": "bytes32",
        "name": "orgId",
        "type": "bytes32"
    },
    {
        "indexed": true,
        "internalType": "address",
        "name": "director",
        "type": "address"
    }
    ],
    "name": "DirectorshipAccepted",
    "type": "event"
},
{
    "anonymous": false,
    "inputs": [
    {
        "indexed": true,
        "internalType": "bytes32",
        "name": "orgId",
        "type": "bytes32"
    },
    {
        "indexed": true,
        "internalType": "address",
        "name": "previousDirector",
        "type": "address"
    },
    {
        "indexed": true,
        "internalType": "address",
        "name": "newDirector",
        "type": "address"
    }
    ],
    "name": "DirectorshipTransferred",
    "type": "event"
},
{
    "anonymous": false,
    "inputs": [
    {
        "indexed": true,
        "internalType": "bytes32",
        "name": "orgId",
        "type": "bytes32"
    },
    {
        "indexed": true,
        "internalType": "bytes32",
        "name": "previousOrgJsonHash",
        "type": "bytes32"
    },
    {
        "indexed": false,
        "internalType": "string",
        "name": "previousOrgJsonUri",
        "type": "string"
    },
    {
        "indexed": false,
        "internalType": "string",
        "name": "previousOrgJsonUriBackup1",
        "type": "string"
    },
    {
        "indexed": false,
        "internalType": "string",
        "name": "previousOrgJsonUriBackup2",
        "type": "string"
    },
    {
        "indexed": true,
        "internalType": "bytes32",
        "name": "newOrgJsonHash",
        "type": "bytes32"
    },
    {
        "indexed": false,
        "internalType": "string",
        "name": "newOrgJsonUri",
        "type": "string"
    },
    {
        "indexed": false,
        "internalType": "string",
        "name": "newOrgJsonUriBackup1",
        "type": "string"
    },
    {
        "indexed": false,
        "internalType": "string",
        "name": "newOrgJsonUriBackup2",
        "type": "string"
    }
    ],
    "name": "OrgJsonChanged",
    "type": "event"
},
{
    "anonymous": false,
    "inputs": [
    {
        "indexed": true,
        "internalType": "bytes32",
        "name": "orgId",
        "type": "bytes32"
    },
    {
        "indexed": false,
        "internalType": "bool",
        "name": "previousState",
        "type": "bool"
    },
    {
        "indexed": false,
        "internalType": "bool",
        "name": "newState",
        "type": "bool"
    }
    ],
    "name": "OrganizationActiveStateChanged",
    "type": "event"
},
{
    "anonymous": false,
    "inputs": [
    {
        "indexed": true,
        "internalType": "bytes32",
        "name": "orgId",
        "type": "bytes32"
    },
    {
        "indexed": true,
        "internalType": "address",
        "name": "owner",
        "type": "address"
    }
    ],
    "name": "OrganizationCreated",
    "type": "event"
},
{
    "anonymous": false,
    "inputs": [
    {
        "indexed": true,
        "internalType": "bytes32",
        "name": "orgId",
        "type": "bytes32"
    },
    {
        "indexed": true,
        "internalType": "address",
        "name": "previousOwner",
        "type": "address"
    },
    {
        "indexed": true,
        "internalType": "address",
        "name": "newOwner",
        "type": "address"
    }
    ],
    "name": "OrganizationOwnershipTransferred",
    "type": "event"
},
{
    "anonymous": false,
    "inputs": [
    {
        "indexed": true,
        "internalType": "address",
        "name": "previousOwner",
        "type": "address"
    },
    {
        "indexed": true,
        "internalType": "address",
        "name": "newOwner",
        "type": "address"
    }
    ],
    "name": "OwnershipTransferred",
    "type": "event"
},
{
    "anonymous": false,
    "inputs": [
    {
        "indexed": true,
        "internalType": "bytes32",
        "name": "parentOrgId",
        "type": "bytes32"
    },
    {
        "indexed": true,
        "internalType": "bytes32",
        "name": "unitOrgId",
        "type": "bytes32"
    },
    {
        "indexed": true,
        "internalType": "address",
        "name": "director",
        "type": "address"
    }
    ],
    "name": "UnitCreated",
    "type": "event"
},
{
    "constant": true,
    "inputs": [],
    "name": "isOwner",
    "outputs": [
    {
        "internalType": "bool",
        "name": "",
        "type": "bool"
    }
    ],
    "payable": false,
    "stateMutability": "view",
    "type": "function"
},
{
    "constant": true,
    "inputs": [],
    "name": "owner",
    "outputs": [
    {
        "internalType": "address",
        "name": "",
        "type": "address"
    }
    ],
    "payable": false,
    "stateMutability": "view",
    "type": "function"
},
{
    "constant": false,
    "inputs": [],
    "name": "renounceOwnership",
    "outputs": [],
    "payable": false,
    "stateMutability": "nonpayable",
    "type": "function"
},
{
    "constant": true,
    "inputs": [
    {
        "internalType": "bytes4",
        "name": "interfaceId",
        "type": "bytes4"
    }
    ],
    "name": "supportsInterface",
    "outputs": [
    {
        "internalType": "bool",
        "name": "",
        "type": "bool"
    }
    ],
    "payable": false,
    "stateMutability": "view",
    "type": "function"
},
{
    "constant": false,
    "inputs": [
    {
        "internalType": "address",
        "name": "newOwner",
        "type": "address"
    }
    ],
    "name": "transferOwnership",
    "outputs": [],
    "payable": false,
    "stateMutability": "nonpayable",
    "type": "function"
},
{
    "constant": false,
    "inputs": [
    {
        "internalType": "address payable",
        "name": "__owner",
        "type": "address"
    }
    ],
    "name": "initialize",
    "outputs": [],
    "payable": false,
    "stateMutability": "nonpayable",
    "type": "function"
},
{
    "constant": false,
    "inputs": [
    {
        "internalType": "bytes32",
        "name": "solt",
        "type": "bytes32"
    },
    {
        "internalType": "bytes32",
        "name": "orgJsonHash",
        "type": "bytes32"
    },
    {
        "internalType": "string",
        "name": "orgJsonUri",
        "type": "string"
    },
    {
        "internalType": "string",
        "name": "orgJsonUriBackup1",
        "type": "string"
    },
    {
        "internalType": "string",
        "name": "orgJsonUriBackup2",
        "type": "string"
    }
    ],
    "name": "createOrganization",
    "outputs": [
    {
        "internalType": "bytes32",
        "name": "id",
        "type": "bytes32"
    }
    ],
    "payable": false,
    "stateMutability": "nonpayable",
    "type": "function"
},
{
    "constant": false,
    "inputs": [
    {
        "internalType": "bytes32",
        "name": "solt",
        "type": "bytes32"
    },
    {
        "internalType": "bytes32",
        "name": "parentOrgId",
        "type": "bytes32"
    },
    {
        "internalType": "address",
        "name": "director",
        "type": "address"
    },
    {
        "internalType": "bytes32",
        "name": "orgJsonHash",
        "type": "bytes32"
    },
    {
        "internalType": "string",
        "name": "orgJsonUri",
        "type": "string"
    },
    {
        "internalType": "string",
        "name": "orgJsonUriBackup1",
        "type": "string"
    },
    {
        "internalType": "string",
        "name": "orgJsonUriBackup2",
        "type": "string"
    }
    ],
    "name": "createUnit",
    "outputs": [
    {
        "internalType": "bytes32",
        "name": "newUnitOrgId",
        "type": "bytes32"
    }
    ],
    "payable": false,
    "stateMutability": "nonpayable",
    "type": "function"
},
{
    "constant": false,
    "inputs": [
    {
        "internalType": "bytes32",
        "name": "orgId",
        "type": "bytes32"
    }
    ],
    "name": "toggleActiveState",
    "outputs": [],
    "payable": false,
    "stateMutability": "nonpayable",
    "type": "function"
},
{
    "constant": false,
    "inputs": [
    {
        "internalType": "bytes32",
        "name": "orgId",
        "type": "bytes32"
    }
    ],
    "name": "acceptDirectorship",
    "outputs": [],
    "payable": false,
    "stateMutability": "nonpayable",
    "type": "function"
},
{
    "constant": false,
    "inputs": [
    {
        "internalType": "bytes32",
        "name": "orgId",
        "type": "bytes32"
    },
    {
        "internalType": "address",
        "name": "newDirector",
        "type": "address"
    }
    ],
    "name": "transferDirectorship",
    "outputs": [],
    "payable": false,
    "stateMutability": "nonpayable",
    "type": "function"
},
{
    "constant": false,
    "inputs": [
    {
        "internalType": "bytes32",
        "name": "orgId",
        "type": "bytes32"
    }
    ],
    "name": "renounceDirectorship",
    "outputs": [],
    "payable": false,
    "stateMutability": "nonpayable",
    "type": "function"
},
{
    "constant": false,
    "inputs": [
    {
        "internalType": "bytes32",
        "name": "orgId",
        "type": "bytes32"
    },
    {
        "internalType": "address",
        "name": "newOwner",
        "type": "address"
    }
    ],
    "name": "transferOrganizationOwnership",
    "outputs": [],
    "payable": false,
    "stateMutability": "nonpayable",
    "type": "function"
},
{
    "constant": false,
    "inputs": [
    {
        "internalType": "bytes32",
        "name": "orgId",
        "type": "bytes32"
    },
    {
        "internalType": "bytes32",
        "name": "orgJsonHash",
        "type": "bytes32"
    },
    {
        "internalType": "string",
        "name": "orgJsonUri",
        "type": "string"
    },
    {
        "internalType": "string",
        "name": "orgJsonUriBackup1",
        "type": "string"
    },
    {
        "internalType": "string",
        "name": "orgJsonUriBackup2",
        "type": "string"
    }
    ],
    "name": "setOrgJson",
    "outputs": [],
    "payable": false,
    "stateMutability": "nonpayable",
    "type": "function"
},
{
    "constant": true,
    "inputs": [
    {
        "internalType": "bool",
        "name": "includeInactive",
        "type": "bool"
    }
    ],
    "name": "getOrganizations",
    "outputs": [
    {
        "internalType": "bytes32[]",
        "name": "",
        "type": "bytes32[]"
    }
    ],
    "payable": false,
    "stateMutability": "view",
    "type": "function"
},
{
    "constant": true,
    "inputs": [
    {
        "internalType": "bytes32",
        "name": "_orgId",
        "type": "bytes32"
    }
    ],
    "name": "getOrganization",
    "outputs": [
    {
        "internalType": "bool",
        "name": "exists",
        "type": "bool"
    },
    {
        "internalType": "bytes32",
        "name": "orgId",
        "type": "bytes32"
    },
    {
        "internalType": "bytes32",
        "name": "orgJsonHash",
        "type": "bytes32"
    },
    {
        "internalType": "string",
        "name": "orgJsonUri",
        "type": "string"
    },
    {
        "internalType": "string",
        "name": "orgJsonUriBackup1",
        "type": "string"
    },
    {
        "internalType": "string",
        "name": "orgJsonUriBackup2",
        "type": "string"
    },
    {
        "internalType": "bytes32",
        "name": "parentOrgId",
        "type": "bytes32"
    },
    {
        "internalType": "address",
        "name": "owner",
        "type": "address"
    },
    {
        "internalType": "address",
        "name": "director",
        "type": "address"
    },
    {
        "internalType": "bool",
        "name": "isActive",
        "type": "bool"
    },
    {
        "internalType": "bool",
        "name": "isDirectorshipAccepted",
        "type": "bool"
    }
    ],
    "payable": false,
    "stateMutability": "view",
    "type": "function"
},
{
    "constant": true,
    "inputs": [
    {
        "internalType": "bytes32",
        "name": "parentOrgId",
        "type": "bytes32"
    },
    {
        "internalType": "bool",
        "name": "includeInactive",
        "type": "bool"
    }
    ],
    "name": "getUnits",
    "outputs": [
    {
        "internalType": "bytes32[]",
        "name": "",
        "type": "bytes32[]"
    }
    ],
    "payable": false,
    "stateMutability": "view",
    "type": "function"
},
{
    "constant": false,
    "inputs": [],
    "name": "setInterfaces",
    "outputs": [],
    "payable": false,
    "stateMutability": "nonpayable",
    "type": "function"
}]
```
