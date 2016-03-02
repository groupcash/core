# Groupcash Algorithms

Implementations of the *groupcash* design should be able to support different cryptographic algorithms for creating and verifying digital signatures.

The current reference implementation is [groupcash/php](https://github.com/groupcash/php) which so far only supports a single algorithm, the Elliptic Curve Cryptography algorithm as implemented in [phpecc](https://github.com/phpecc/phpecc).

The goal of this document is to present a specification of different cryptographic algorithms that implementations should support.