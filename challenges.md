# Challenges and Assumptions for Groupcash Currencies

[work in progress]

There are several requirements for this system to work.

### Available computers

Since transactions rely of cryptographic signatures, participants require a computer to make transactions. For validating the transaction, a connection to the backer is needed. In order to use the currency of the go, both both assets need to be mobile.

Computers can be avoided by printing *blank* transactions that can be claimed by anyone and therefore can be used like paper bills but increase the risk of fraud through double-spending.

### Reliable signatures

In order for the signatures to be reliable, the following is needed
- a collision-free, secure hashing algorithms
- a future-proof trapdoor function
- a reliable source of randomness

### Secure private keys

The private keys of all participants must remain private. If a private key is stolen, the victim can lose all their unspent units.

### Market acceptance

The currency requires are sufficient number of units for trade and possibilities to spend them. This depends on the number of backers and their willingness to issue promises. It must also be accepted by merchants and consumers.

### Enforceability of signatures

The signed promises must be enforceable, meaning the proven owner of the promise must have a right to receive the promised delivery.