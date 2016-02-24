# Data Structures

This document described the data structures that the proposed currency system is based on. These structures allow to **issue** coins, **transfer** their ownership and **confirm** them, i.e. avoid double spending, without a central database.

The data structures and their graphical representations are a adopted from the [bitcoin] whitepaper.

[bitcoin]: https://bitcoin.org/bitcoin.pdf

## Transactions

A *coin* is a chain of transactions, each transferring the ownership of the previous one to a new target. This is done by signing the targets public key together with the hash of the previous transaction with the private key of the owner, as shown is the following figure.

![Transaction chain](figures/chain.svg)

## Genesis

The beginning of the chain is formed by the *issue* transaction which is signed indirectly by the regulatory entity with the private key of the currency. The regulator of the currency can authorize issuers to distribute the issuing without having to share the currency's private key.

The issue signs the description of a delivery promise that the coin is backed by together with the public key of the backer and the value of the promise in currency units, as shown in the following figure.

![Coin Issue](figures/issue.svg)

It is the issuer's responsibility to make sure that the promise is legit and to determine its worth in the given currency.

## Transferring Values

Each transaction can refer to multiple previous transactions, called *inputs* and also transfer different parts of its input to several targets, called *outputs*. Each input references an output of another transaction whereas all referenced outputs must have the same target.

As depicted in the following figure, the owner (the target of the references outputs) signs the hash of all inputs and outputs.

![Coin Transaction](figures/transaction.svg)

The sum of all output values must equal the sum of all input values. If it's smaller, currency units are lost since every output can only be referenced by one input to make sure that every transaction has a unique hash value.

## Confirmation

Because each transaction can have multiple inputs, a coin is the root of a transaction tree, consisting of overlapping chains between an *issue* and the coin as illustrated in the following figure.

![Transaction Tree](figures/tree.svg)

If this chain is longer than one transaction, a fraudulent participant could reference his output with more than one input, effectively double-spending the coin. To make sure that this hasn't happened, the chain needs to be *confirmed* by the backer of the issue.

The backers verify the consistency of the transaction chains and make sure that no transaction referencing any output of the involved transactions has already been confirmed. Each backer creates then a new coin with a *confirmation* transaction, transferring their proportion of the original coin to its owner. In order to preserve the uniqueness of each transaction, the hash of the root of the confirmed tree is included in the confirmation. The following figure show the resulting coins.

![Confirmation Result](figures/confirmation.svg)

In the example, the backers **A** and **B** transfer `5` and `7` units to **D** respectively and the backer **C** transfers `8` units to **E**. These transfer parts of their received units to **F** which in turn transfers `8` units to **G**. In order to confirm it, **G** has to send the coin to **A**, **B** and **C**. These make new transferences proportional to the value of their promises. Since **A**'s promise is worth 5 units, they transfer `5 * 8 / (5+7+8) = 2` units to **G**. The other backer are doing likewise and the result is three coins with a combined value of `8`.

If a backer confirms a coin by mistake, then the total value of coins based on their promise and therefore their liability increases without receiving compensation. Otherwise if a backer refuses to confirm a coin, the owner of the coin can demand to be shown the transaction transferring an output of their chain to another input. Therefore it exists a mutual enforceability of demands assuming that no private key was compromised.