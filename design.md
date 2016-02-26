# Design

This document describes the data structures and their transformations that the proposed currency system is based on. These structures allow to **issue** new coins, **transfer** their ownership and **confirm** them (to avoid double spending) without a central database.

The structures and their graphical representations are a adopted from the [bitcoin] whitepaper.

[bitcoin]: https://bitcoin.org/bitcoin.pdf

## Transactions

A *Coin* is a chain of *Transactions*, each transferring the ownership of the previous one to the public key of a new *Target* owner. This is done by signing the Target's public key together with the hash of the previous Transaction with the private key of the owner, as shown is the following figure.

![Transaction chain](https://cdn.rawgit.com/groupcash/core/a818238/figures/chain.svg)

## Genesis

The beginning of the chain is formed by the *Base* Transaction which is signed indirectly by the regulatory entity with the private key of the *Currency*. The regulator of the Currency can authorize *Issuers* to distribute the task of issuing coins without having to share the Currency's private key.

The Issuer signs the description of a delivery *Promise* that the Coin is backed by, together with the public key of the *Backer* and the *Value* of the Promise in currency units. The structure of the *Authorization*, the Promise and the Base is shown in the following figure.

![Coin Base](https://cdn.rawgit.com/groupcash/core/a818238/figures/base.svg?1)

It is the Issuer's responsibility to make sure that the Promise is legit and to determine its worth in the given currency. Since the signatures rely on hashes, the Promise must be unique per Backer and Issuer to avoid two Bases with the same hash.

## Transferring Values

Each Transaction can refer to multiple previous Transactions, called *Inputs* and also transfer different parts of its Input to several Targets, called *Outputs*. Each Input references one Output of another Transaction whereas all referenced Outputs must have the same Target.

As depicted in the following figure, the owner (the common Target of the referenced Outputs) signs the hash of all Inputs and Outputs.

![Coin Transaction](https://cdn.rawgit.com/groupcash/core/a818238/figures/transaction.svg)

The sum of all Output values must equal the sum of all Input values. If it's smaller, currency units are lost since every Output can only be referenced by one Input to make sure that every Transaction has a unique hash value.

## Confirmation

Because each Transaction can have multiple Inputs, a Coin is the root of a Transaction tree, consisting of overlapping chains between the Coin and its Bases as illustrated in the following figure.

![Transaction Tree](https://cdn.rawgit.com/groupcash/core/a818238/figures/tree.svg)

If a chain is longer than one Transaction, a fraudulent participant could reference his Output with more than one Input, effectively double-spending the Coin. To make sure that this hasn't happened, a Target needs to confirm the validity of the Coin. This is done by the Backers of the Bases at the leafs of the tree.

The Backers verify the consistency of all Transaction chains and make sure that no Transaction referencing any Output of the involved Transactions has already been confirmed by them. Each Backer creates then a new Coin with a *Confirmation* Transaction, transferring their proportion of the original Coin to its Owner.

In order to preserve the uniqueness of each Transaction, the hash of the root of the confirmed tree is included in the Confirmation. The following figure show the resulting Coins.

![Confirmation Result](https://cdn.rawgit.com/groupcash/core/a818238/figures/confirmation.svg)

In the example, the Backers **A** and **B** transfer `4` and `2` units to **D** respectively and the Backer **C** transfers `7` units to **E**. **D** and **E** transfer parts of their received units to **F** which in turn transfers `8` units to **G**. In order to confirm these transactions, **G** has to send the Coin to **A**, **B** and **C**. These make new Transferences to **G** with a value proportional to the value of their promises. Since **A**'s promise is worth `5` units, they transfer `5 * 8 / (5+7+8) = 2` units to **G**. The other Backers are doing likewise which results in three Coins with a combined value of `8`.
