# Groupcash Formats

The goal of this document is to specify how objects of the *groupcash* design (currently Coin and Authorization) can be represented for storage and transport between applications. The current reference implementation is [groupcash/php](https://github.com/groupcash/php).

Serialization is done in three steps:

1. **Transformation** defines the structure and types of an object representation
2. **Serialization** brings flattens this structure (json, msgpack).
3. **Encoding** is applied to binary data (hex, base64).