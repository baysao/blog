---
title: "UTXO vs Account"
summary: UTXO vs Account
date: 2022-09-26
series: ["blockchain"]
weight: 1
tags: ["blockchain"]
author: "baysao"
---

# Background

Blockchains solve the problem of deciding which chain is valid with the use of consensus algorithms. Consensus algorithms combine cryptography and economic incentives to enforce correctness and immutability. Decentralized consensus distinguishes public blockchains from predecessor technology such as linked lists or shared databases.

# Ledger Data

Blockchains provide a way for adversaries to agree on the current global state in a peer-to-peer manner.
All cryptocurrencies start with a genesis state, and then each block includes transactions that move the state forward.

# UTXO based

This is the original form of a blockchain used by Bitcoin and many Bitcoin derivatives such as Zcash and Litecoin.
In a UTXO-based ledger, strictly speaking, there are no accounts or wallets at the protocol layer. Instead, coins are stored as a list of unspent transaction outputs or UTXOs.
Each UTXO has a quantity and criteria for spending it. Transactions are created by consuming existing UTXOs and producing new UTXOs in their place.

- A UTXO is akin to a pile of coins that gets transferred by satisfying the current spending criteria. UTXOs can be divided or combined to create the denomination needed for a particular transaction.

## Advantages:

- Simplicity. Spending a UTXO is all or nothing. Since UTXOs are uniquely referenced and completely consumed upon spending, there is no chance for a transaction to be replayed.

- Transactions can be trivially verified in parallel. It is impossible for two transactions to affect the same UTXO. This is due to the stateless nature of UTXO transactions. Transactions do not refer to any input outside of the UTXOs consumed and corresponding signatures.

- Privacy-preserving behavior is encouraged in the UTXO model. Users are encouraged to generate a new address for every incoming transaction including changing addresses. By using a new address each time, it is difficult to definitively link different coins to a single owner.

## Disadvantages:

- UI/UX considerations are tricky. Users tend to think of accounts when they conceptualize their money. Since there is no concept of an account within Bitcoin, it is up to the wallet provider to manage a potential set of addresses and sum the corresponding balances. Doing so in a privacy-preserving way may require running a local node.
- Smart contracting abilities are quite limited in a UTXO model. Each UTXO has spending criteria that dictate spending conditions. This can require signatures from multiple parties, but there is little ability to reference outside states such as oracles.

# Account-based models

Rather than following in Bitcoin’s footsteps, smart contract focus blockchains have chosen to employ an account strategy. Instead of having each coin be uniquely referenced, coins are represented as a balance within an account. Accounts can either be controlled by a private key or a smart contract.

One important difference between UTXO-based blockchains and account-based blockchains is that UTXO transactions specify the resulting state exactly. We know what the result will be when we apply the transaction. The resulting coin locations are embedded in the transaction itself. This is not so with an account-based system. Transactions in an account-based system rely on existing states and are therefore known as stateful. This allows more flexibility with the expense of more moving parts.

To illustrate some of the nuance introduced in an account-based model, consider that balances can be partially spent in an account model. If I have 100 ETH, I can send you 5 ETH and the result is that I have 95 ETH and you have 5 ETH. If the system is not carefully designed, that transaction could be replayed resulting in me having 90 ETH and you having 10 ETH, despite the sender’s intention to have the transaction applied only once. To avoid this, an incrementing nonce is required to ensure that transactions are not processed multiple times.

## Advantages

More flexible transactions. Transactions depend on the existing state and can have diverging effects based on external input. This allows things like oracles and other logic to influence the resulting state of a transaction.
Transactions do not explicitly include the resulting state resulting in smaller transaction sizes.

## Disadvantages

Because the result of a transaction depends on the input state, care must be taken when executing transactions in parallel. Generally, transactions affecting the same account will need to be executed one after another.
Account models encourage address reuse which is generally a detriment to privacy since the account itself links transactions together to a single owner.
