# Algorithms

This document proposes three core algorithms to create and transform currency units, referred to as *coins*. Furthermore it contains two auxiliary algorithms and finally it describes how these algorithms are used in different cases.


## Core Algorithms

The most important actions for managing the currency are to **issue** new coins, **transfer** coins to new owners and **validate** the legitimacy of transferred coins.

Although these are formal descriptions, they are not complete and therefore sufficient for implementation.

### Issue Coin

An issued coin is worth one currency unit can be denoted as  
`coin(A, i) = sign(R, (P_A, i, K_A))`  where  
`sign(Y, X) = (X, hash(X) ^ PK_Y)` is `X` signed by `Y`  
`PK_R` is the private key of `R`  
`R` is the regulatory entity  
`hash(X)` is the cryptographic hash of `X`  
`P_A` is a delivery promise by `A` worth one unit  
`A` is a backing entity  
`i` is the serial number of the coin  
`K_A` is the public key of `A`  

### Transfer Coin

A fraction `F` of coin `COIN` is transferred from its current owner to a target `B` with  
`trans(COIN, B, F) = sign(A, (COIN, K_B, F))` where  
`F = ]0:1]`  

### Validate Coin

Transferred coins are recursively validated by the backer `A` with  
`valid(trans(COIN, C, F), A) = sign(A, (P, K_C, F * fract(P), hash(P)))` with  
`P = prev(valid(COIN, A))` where  
`prev(trans(COIN, A, F)) = COIN` and  
`fract(trans(COIN, A, F)) = F`  
the terminating case is `valid(coin(A, i)) = trans(coin(A, i), nil, 1)`



## Auxiliary Algorithms

The following sections contain informal descriptions of how to **verify** the integrity of a coin and **resolve** the balance changes after one or several transferences.

### Verify Coin

A coin can be verified successfully if all of the following criteria are met

- The issuer of the coin is an accepted regulatory entity of the currency
- The signature of the issuer is valid
- The signature if each transaction is valid
- The signer of each transaction is the target of the previous transaction

A signature is valid if the actually used private key can be confirmed to belong to the stated public key the signer.


### Resolve Transactions

Backers can only validate transactions after they made sure that the transferring users were indeed in possession of the transferred coin or fraction of the coin. To do so, the resulting balance changes of all transactions of a coin have to resolved.

This can be done by 

- iterating through all transactions
- calculate transferred fraction as fraction of the previous transaction times fraction of the current transaction
- increase balance of target by fraction
- decrease balance of previous owner by fraction

The sum of all balances must always be zero.



## Use cases

### Genesis

`R` and `A` decide on `P_A` -- the promised delivery by `A` per unit   
`R` determines `X_A` -- the number of currency units plausibly backed by `A`  
`R` publishes `sign(R, (A, K_A, P_A, X_A))`  
`R` sends `CiA = coin(A, i)` to `K_A` with `i=[1;X_A]`  

### Buying

`B` gets list of all backers from `R`, including `K_A`  
`B` requests `X` units from `K_A`  
`A` sends `CiAB = trans(CiA, K_B, F)` to `K_B` with `i=[n;n+X]`  

### Transfer

`B` sends `CiAB_C = trans(CiAB, K_C, F)` to `K_A` for validation  
`A` verifies the coin and makes sure that `B` is its owner  
`A` sends `CiABC = valid(AiAB_C)` to `K_B`  
`B` sends `CiABC` to `K_C`  

### Offline transfer

`B` sends `CiAB_C` to `K_C`  
`C` sends `CiAB_C` to `K_A` for validation  
`A` sends `CiABC` to `K_C`



## Optimizations

Experiments have shown that the size of a validated coin is approximately 2KB. When transferring large numbers of coins, it should be possible to decrease the necessary amount of data. One way could be to combine coins into a single transaction, another to reference a URL instead of inlining the promise description, or only including it once.
