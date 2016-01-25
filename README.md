# Groupcash: A Complementary Commodity-Backed Cryptographic Community Currency

This text describes a virtual complementary currency, relying on contracts concluded with cryptographic signatures and backed by delivery promises of value-creating community members. The compatibility and plausibility of these promises is verified by a regulatory mechanism. The proposal is inspired by cryptographic and local currencies.


## Design goals

### Clear value concept

While currencies used to be commodity-backed (e.g. gold standard), this is not any more the case for most. Hence the value of these "political" currencies is mainly make-belief. It's derived from what people believe it's worth and how much they think it will be worth in the future. It also depends on how much they trust the government that is guaranteeing the value. A goal of the proposed currency must be that each participant can easily understand and estimate the value of each currency unit.

### Low fluctuation

Fluctuating currencies are prone to be hoarded by investors hoping to make profit. A goal of the proposed currency should be to incentivise circulation and decrease fluctuation. This is compatible with the goal of clear value proposition.

### High velocity

The currency should provide an incentive to keep circulation going. Thus preventing deflation by hoarding and further stabilizing its value.

### Decentralization

The creation of traditional, political currencies lies in the hand of a single government body. Double-spending is avoided through counterfeit-proof tokens (cash) and accounts managed by a few banks. The proposed currency should use a community to collectively create spendable units and prohibit double-spending. The participants should also be able to transfer units independently if wished.

### No transaction fees

High transaction fees harm the economy since they decrease the practical size of transactions. The proposed currency should enable transaction to very low or no costs. The goal of decentralization supports this as well.

### Built on trust

While the main proposition of crypto-currencies like Bitcoin is that no trust is required between the participants in order to trade, this also creates purely profit-driven incentives to participate. In a completely unregulated market, this naturally leads to quasi-monopolies. The proposed currency should provide its users gains from trust each other and make sure that the self-interest of its participants does not contradict the common interest of the community.



## Implementation

### Useful commodities

The proposed currency is representative, i.e. directly backed by useful commodities. It's units are delivery promise by a value-creating entity. What counts as "useful" must be defined by the community but ideally it would be something with intrinsic value like food, energy or workforce as opposed to merely "rare" substances like gold. Since each unit represents a promise directly, users can decide themselves which commodities they find useful and which backers trust-worthy.

## Regulation

To make sure that the promises comply with the above mentioned definition and also to limit the risk that the backer will not be able to fulfil their promises, a regulatory mechanism is required. This mechanism must make sure that a backer does not sell more promises than they are likely to be able to deliver within a given time frame. For example, a rule could be that a maximum of 10% of the yearly output can be promised. The regulation could either be performed by an organisation or by the community itself.

## Cryptographic signatures

To enable decentralization, public/private key pairs are used to sign contracts like promises and transactions. Public keys serve as pseudonyms and addresses of the participants.
While spending units still relies on the validation of the backer, they cannot change your "balance" without your signature.

## Fixed prices

While units can be sold and bought on the open market, backers should guarantee a fixed price. For example $1 per unit. They should also guarantee to buy-back their promises although they can keep a margin.



## Incentives

For each type of user, an incentive must exist to participate in the currency. These incentives must not compromise the common goals described above.

### Backer

Value-creating entities become backers by issuing delivery promises. These promises are most probably never demanded so selling these promises is a source of capital for the backers which can be invested. They also gain a margin when buying back their promises.

The backer also has an incentive to prevent double-spending since that would increase the demandable deliveries without receiving compensation.

### Regulator

The regulator bears the costs of acquiring new backers, assuring their compatibility, determining the delivery promise equivalent to one unit and calculating the maximum number of units they may issue. This could be compensated by a fee for validating the created units, decreasing the sell/buy margin of the backers. Another source of income could be to manage the accounts of the backers, either charging for this service or by keeping the margins.

### Merchant

By accepting the proposed currency, merchants benefit from a faster, more secure and cheaper mean of payment. Because of the guaranteed buy-back by the backers, the risk is the buy/sell margin and thus small and calculate-able.

### Consumer

Consumers benefit from a faster, cheaper way of payment as well. Because of the fixed prices, units can be bought with no loss.



## Protocol

The following is a informal description of the communication between the participants in different use cases.

### Participants

`A` -- value producing entity  
`B` -- consumer  
`C` -- consumer  
`D` -- consumer  
`R` -- regulatory entity

### Nomenclature

`K_I` -- Public key of `I`, pseudonym and address of `I`  
`PK_I` -- Private key of `I`, must be kept secret  
`H(X)` -- Cryptographic hash of `X`  
`S_I(X) = (X, H(X)*PK_I)` -- `X` signed by `I`  
`Ci_A` -- a unit ("coin") with the serial number `i` issued by `A`  
`Ci_AB` -- `Ci_A` transfered to `K_B`, validated by `K_A`  
`Ci_AB_C` -- `Ci_AB` transfered to `K_C` but not yet validated

### Use cases

#### Genesis

`R` and `A` decide on `P_A` -- the promised delivery by `K_A` per unit  
`R` determines `X_A` -- number of currency units plausibly backed by `A`  
`R` publishes `S_R(A, K_A, P_A, X_A)`  
`R` sends `Ci_A = S_R(P_A, i)` to `K_A` with `i=[1;X_A]`  

#### Buying `A` -> `B`

`B` gets list of all backers from `R`, including `K_A`  
`B` requests `X` units from `K_A`  
`A` sends `Ci_AB = S_A(Ci_A, K_B)` to `K_B` with `i=[1;X]`  

#### First Transfer `B` -> `C`

`B` sends `Ci_AB_C = S_B(Ci_AB, K_C)` to `K_A`  
`A` sends `Ci_ABC = S_A(Ci_A, K_C, H(Ci_AB))` to `K_C`  

#### Alternative transfer `B` -> `C`

`B` sends `Ci_AB_C` to `K_C`  
`C` sends `Ci_AB_C` to `K_A`  
`A` sends `Ci_ABC` to `K_C`

#### Following Transfer `C` -> `D`

`C` sends `Ci_ABC_D = S_C(Ci_ABC, K_D)` to `K_A`  
`A` sends `Ci_ABCD = S_A(Ci_A, K_D, H(Ci_ABC))` to `K_D`  

#### Selling `D` -> `A`

`D` sends `Ci_ABCD_A = S_D(Ci_ABCD, K_A)` to `K_A`  



## Optimizations

It should be possible to transfer a fraction of a unit and also to minimize the amount of data required to transfer a large amount of units. How this can be implemented still has to be determined. Another way to decrease the data size is to reference the promise instead of transferring it with every transaction. The former might still be desirable in case of low or no connectivity.



## Assumptions

### Reliable signatures

In order for the signatures to be reliable, the following is needed
- a collision-free, secure hashing algorithms
- a future-proof trapdoor function
- a reliable source of randomness

### Secure private keys

The private keys of all participants must remain private. If a private key is stolen, the victim can lose all their unspend units.

### Market acceptance

The currency requires are sufficient number of unit for trade. This depends on the number of backers and their willingness to issue promises. It must also be accepted by merchants and consumers.

### Enforceability of signatures

The signed promises must be enforceable, meaning the proven owner of the promise must have a right to receive the promised delivery.



## Attacks

This is an incomplete list of possible attacks and how the cryptographic system protects the participants.

### Faking ownership

After `C` has transferred ownership of `Ci_ABC` to `K_D`, they could demand delivery of `P_A` from `A`. If `A` has not validated the transaction yet, they have no way to know that `K_C` is not the rightful owner. After validation, `A` is in possession of `Ci_ABC_D` to prove that the transaction was ordered by `K_D`.

### Double-spending

The only way to make sure that a unit hasn't been transferred before is to ask the backer to validate the transaction. In case this is not possible because of a lack of connectivity, the transaction can still be accepted and validated later if the receiver trusts the sender.
