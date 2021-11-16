---
layout: default
title: From where can I get Líf tokens?
permalink: /docs/payment/lif-token/
parent: Payments
nav_order: 4
---

# From where can I get Líf tokens?

## Using Uniswap

The Líf token can be purchased on the Uniswap exchange.

### Uniswap pre-requisites

To interact with the Uniswap exchange, you will need:

1. An Ethereum wallet such as [Metamask](https://metamask.io/download.html)
2. Another token accepted by Uniswap to exchange, such as ETH, USDT, USDC, ...
3. A small amount of Ether available to pay the transaction fee.
4. Make sure the Lif token is configured in your wallet, you might need to add a custom token using these values:

| Network | Mainnet |
|-|-|-|-|
| Address | 0x9C38688E5ACB9eD6049c8502650db5Ac8Ef96465 |
| Symbol | LIF |
| Decimals | 18 |

### Uniswap steps

1. Open to the [Uniswap application](https://app.uniswap.org/)
2. Connect your Ethereum wallet
3. When selecting a token, by default Uniswap will load the *Uniswap Default List*. In the bottom right corner, click on **Change** to change the Token List.
4. Select the **Kleros T2CR** token list. This is a list curated by the [Kleros project](https://kleros.io) where Líf is included.
5. Search for the LIF token and select it
6. Enter the amount of desired LIF token
7. If the token you are exchanging requires an approval, you will be invited to approve Uniswap as an authorized spender
8. Click on Swap and confirm the transaction in your wallet

<!--
*Hint*: In the Ropsten test system, Uniswap is also available. Just switch your Ethereum wallet to the Ropsten test system and at step 4 use [this Ropsten-crafted custom list](https://gist.githubusercontent.com/mtahon/40dbb2fd2104a59b6bfa3e896addd287/raw/f16b8dfc023056249a4778828aba2848803d7990/token_list.json)

## Using the Lif Faucet in Ropsten test environment

### LÍF Faucet pre-requisites

To interact with the Uniswap exchange, you will need:

1. An Ethereum wallet such as [Metamask](https://metamask.io/download.html)
2. A small amount of Ropsten Ether available to pay the transaction fee.
3. Make sure the Líf token is configured in your wallet, you might need to add a custom token using these values:

| Network | Ropsten |
|-|-|-|-|-|
| Address |  0xB6e225194a1C892770c43D4B529841C99b3DA1d7 |
| Symbol | LIF |
| Decimals | 18 |

### Receive some Ropsten Ether

Ropsten Ether can be received using a faucet such as the following, just provide the address of your wallet to be deposited:

* Dimension Network: [https://faucet.dimensions.network/](https://faucet.dimensions.network/)
* Defi Karen: [https://faucet.ropsten.be/](https://faucet.ropsten.be/)

### Receive some Ropsten Líf

1. Open the [Etherscan Contract](https://ropsten.etherscan.io/address/0xB6e225194a1C892770c43D4B529841C99b3DA1d7#writeContract) of the Líf contract
2. Click on *Connect to Web3* and connect your Ethereum wallet
3. Locate the *11. Faucet Lif* function and click on **Write**
4. Approve the transaction in your Ethereum wallet
5. Once your transaction is mined, your wallet will be toped-up to 50 Líf

*Hint*: The Faucet tops-up your balance to 50 Líf, if you already have some Ropsten Líf you will receive the difference so that your balance is 50.
-->
