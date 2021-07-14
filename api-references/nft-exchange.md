---
description: >-
  NFT decentralized non-custodial marketplace will facilitate P2P trading
  between sellers andbuyers. The process will be controlled by the
  ExchangeManager contract. It will provide thefollowing functi
---

# NFT Exchange

### createTrade:

**Inputs:**

* NFT address, the tokenID
* Address in which they want to get paid and the amount
* Expiration date .

**Output:**

* Tx ID

This function will be used by sellers to list a new trade opportunity.

When called, the user will be asked to approve the transaction, and the NFTs will be transferred

to the smart contract . The function will generate a unique trade ID.

### Purchase

**Input:**

* Tx ID

This function will be called by buyers to perform a trade by sending the trade ID. The function

will get the tokens to pay with from them, they need to approve them first, collect a fee, and

send the rest to the seller.At the same time, it will send the NFTs to the buyer. The trade is then marked as completed.

### expireTrade:

**Input:**

* Tx ID

This function can be called by a seller to expire a non fulfilled trade to recover their NFT token.

### withdrawFees: 

The administrator of the smart contract can call this function to withdraw fees.

### ListTrades:

**Inputs:** None

**Outputs:** List of available NFT for sale with details.

