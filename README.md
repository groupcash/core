# Groupcash: A Commodity-Backed Cryptographic Community Currency

This text describes a virtual complementary currency, relying on contracts concluded with cryptographic signatures and backed by delivery promises of value-creating community members. The compatibility and plausibility of these promises is verified by a regulatory mechanism. The proposal is inspired by cryptographic and local currencies.


## Design goals

### Clear value concept

While currencies used to be commodity-backed (e.g. gold standard), this is not any more the case for most. Hence the value of these "political" currencies is mainly make-belief. It's derived from what people believe it's worth and how much they think it will be worth in the future. It also depends on how much they trust the government that is guaranteeing the value. A goal of the proposed currency must be that each participant can easily understand and estimate the value of each currency unit.

### Low fluctuation

Fluctuating exchange rates of currencies cause it to be hoarded by investors hoping to make profit. A goal of the proposed currency should be to incentivise circulation and decrease fluctuation. This is compatible with the goal of clear value proposition.

### High velocity

The currency should provide an incentive to keep circulation going, for example by introducing an artificial inflation. Thus preventing hoarding which could lead to a shortage of tradable units and further stabilizing its value.

### Decentralization

The creation of traditional, political currencies lies in the hand of a single government body. Double-spending is avoided through counterfeit-proof tokens (cash) and accounts managed by a few banks. The proposed currency should use a community to collectively create spendable units and prohibit double-spending. The participants should also be able to transfer units independently if wished.

### No transaction fees

High transaction fees harm the economy since they decrease the practical size of transactions. The proposed currency should enable transaction to very low or no costs. The goal of decentralization supports this as well.

### Built on trust

While the main proposition of crypto-currencies like Bitcoin is that no trust is required between the participants in order to trade, this also creates purely profit-driven incentives to participate. In a completely unregulated market, this naturally leads to quasi-monopolies. The proposed currency should provide its users gains from trusting each other and make sure that the self-interest of its participants does not contradict the common interest of the community.



## Implementation

### Useful commodities

The proposed currency is representative, i.e. directly backed by useful commodities. It's units are delivery promises by value-creating entities. What counts as "useful" must be defined by the community but ideally it would be something with intrinsic value like food, energy or workforce as opposed to merely "rare" substances like gold. Since each unit represents a promise directly, users can decide themselves which commodities they find useful and which backers trust-worthy.

### Regulation

To make sure that the promises comply with the above mentioned definition and also to limit the risk that the backer will not be able to fulfil their promises, a regulatory mechanism is required. This mechanism must make sure that a backer does not sell more promises than they are likely to be able to deliver within a given time frame. For example, a rule could be that a maximum of 10% of the yearly output can be promised. The regulation could either be performed by an organisation or by the community itself.

### Cryptographic signatures

To enable decentralization, public/private key pairs are used to sign contracts like promises and transactions. Public keys serve as pseudonyms and addresses of the participants.
While spending units still relies on the validation of the backer, they cannot change your "balance" without your signature.

### Fixed prices

While units can be sold and bought on the open market, backers should guarantee a fixed price. For example $1 per unit. They should also guarantee to buy-back their promises although they can keep a margin.



## Incentives

For each type of user, an incentive must exist to participate in the currency. These incentives must not compromise the common goals described above.

### Backer

Value-creating entities become backers by making delivery promises. These promises are most probably never demanded so selling these promises is a source of capital for the backers which can be invested. Since they receive this loan by a large number of people, the result a kind of crowd-funding. Backers can also gain a margin when buying back their promises.

A backer also has an incentive to prevent double-spending since that would increase the demandable deliveries without receiving compensation. This is done by "validating" a transferred coin.

### Regulator

The regulator bears the costs of acquiring new backers, assuring their compatibility, determining the delivery promise equivalent to one unit and calculating the maximum number of units they may issue. This could be compensated by a fee per created units, decreasing the sell/buy margin of the backers. Another source of revenue could be to manage the accounts of the backers, either charging for this service or keeping the margins.

### Merchant

By accepting the proposed currency, merchants benefit from a faster, more secure and cheaper mean of payment. Because of the guaranteed buy-back by the backers, the only risk is the buy/sell margin and thus small and calculate-able.

### Consumer

Consumers benefit from a faster, cheaper way of payment as well. Because of the fixed prices, units can be bought with no loss.



## Protocol

The following is a semi-formal description of the communication between the participants of the currency.


### Definitions

#### Issued Coin

An issued "coin" worth one currency unit can be denoted as  
`coin(A, i) = sign(R, (P_A, i, K_A))`  where  
`sign(Y, X) = (X, hash(X) ^ PK_Y)` is `X` signed by `Y`  
`PK_R` is the private key of `R`  
`R` is the regulatory entity  
`hash(X)` is a cryptographic hash of `X`  
`P_A` is a delivery promise by `A` worth one unit  
`A` is a backing entity  
`i` is the serial number of the coin  
`K_A` is the public key of `A`  

#### Transferred Coin

A fraction `F` of coin `COIN` is transferred from its current owner to a target `B` with  
`trans(COIN, B, F) = sign(A, (COIN, K_B, F))` where  
`F = ]0:1]`

#### Validated Coin

Transferred coins are recursively validated by the backer `A` with  
`valid(trans(COIN, C, F), A) = sign(A, (P, K_C, F * fract(P), hash(P)))` with  
`P = prev(valid(COIN, A))` where  
`prev(trans(COIN, A, F)) = COIN` and  
`fract(trans(COIN, A, F)) = F`  
the terminating case is `valid(coin(A, i)) = trans(coin(A, i), nil, 1)`


### Use cases

#### Genesis

`R` and `A` decide on `P_A` -- the promised delivery by `A` per unit   
`R` determines `X_A` -- the number of currency units plausibly backed by `A`  
`R` publishes `sign(R, (A, K_A, P_A, X_A))`  
`R` sends `CiA = coin(A, i)` to `K_A` with `i=[1;X_A]`  

#### Buying

`B` gets list of all backers from `R`, including `K_A`  
`B` requests `X` units from `K_A`  
`A` sends `CiAB = trans(CiA, K_B, F)` to `K_B` with `i=[n;n+X]`  

#### Transfer

`B` sends `CiAB_C = trans(CiAB, K_C, F)` to `K_A` for validation  
`A` sends `CiABC = valid(AiAB_C)` to `K_B`  
`B` sends `CiABC` to `K_C`  

#### Offline transfer

`B` sends `CiAB_C` to `K_C`  
`C` sends `CiAB_C` to `K_A` for validation  
`A` sends `CiABC` to `K_C`



## Optimizations

Experiments have shown that the size of a validated coin is approximately 2KB. When transferring large numbers of coins, it should be possible to decrease the necessary amount of data. One way could be to combine coins into a single transaction, another to reference a URL instead of inlining the promise description, or only including it once.



## Assumptions

### Reliable signatures

In order for the signatures to be reliable, the following is needed
- a collision-free, secure hashing algorithms
- a future-proof trapdoor function
- a reliable source of randomness

### Secure private keys

The private keys of all participants must remain private. If a private key is stolen, the victim can lose all their unspent units.

### Market acceptance

The currency requires are sufficient number of unit for trade. This depends on the number of backers and their willingness to issue promises. It must also be accepted by merchants and consumers.

### Enforceability of signatures

The signed promises must be enforceable, meaning the proven owner of the promise must have a right to receive the promised delivery.



## Attacks

This is an incomplete list of possible attacks and how the cryptographic system protects the participants.

### Faking ownership

After `B` has transferred ownership of `CiABC` to `K_C`, they could demand delivery of `P_A` from `A`. If `A` has not validated the transaction yet, they have no way to know that `K_B` is not the rightful owner. After validation, `A` is in possession of `CiAB_C` to prove that the transaction was ordered by `K_B`.

### Double-spending

The only way to make sure that a unit hasn't been transferred before is to ask the backer to validate the transaction. In case this is not possible because of a lack of connectivity, the transaction can still be accepted and validated later if the receiver trusts the sender.
